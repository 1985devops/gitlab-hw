# Домашнее задание к занятию 2 «Кластеризация и балансировка нагрузки» -  Нугаев Алексей


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

1. `Запустил два simple python сервера на ubuntu  на разных портах 8081 и 8082`
2. `Установил HAProxy, воспользуйтесь материалами к лекции по ссылке и настроил балансировку Round-robin на 4 уровне`

```
global
        log /dev/log    local0
        log /dev/log    local1 notice
        chroot /var/lib/haproxy
        stats socket /run/haproxy/admin.sock mode 660 level admin expose-fd listeners
        stats timeout 30s
        user haproxy
        group haproxy
        daemon

        # Default SSL material locations
        ca-base /etc/ssl/certs
        crt-base /etc/ssl/private

        # See: https://ssl-config.mozilla.org/#server=haproxy&server-version=2.0.3&config=intermediate
        ssl-default-bind-ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM>
        ssl-default-bind-ciphersuites TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256
        ssl-default-bind-options ssl-min-ver TLSv1.2 no-tls-tickets


defaults
        log     global
        mode    http
        option  httplog
        option  dontlognull
        timeout connect 5000
        timeout client  50000
        timeout server  50000
        errorfile 400 /etc/haproxy/errors/400.http
        errorfile 403 /etc/haproxy/errors/403.http
        errorfile 408 /etc/haproxy/errors/408.http
        errorfile 500 /etc/haproxy/errors/500.http
        errorfile 502 /etc/haproxy/errors/502.http
        errorfile 503 /etc/haproxy/errors/503.http
        errorfile 504 /etc/haproxy/errors/504.http

listen stats  # веб-страница со статистикой
        bind                    :888
        mode                    http
        stats                   enable
        stats uri               /stats
        stats refresh           5s
        stats realm             Haproxy\ Statistics

frontend example  # секция фронтенд
        mode http
        bind :8088
        #default_backend web_servers
        acl ACL_example.com hdr(host) -i example.com
        use_backend web_servers if ACL_example.com

backend web_servers    # секция бэкенд
        mode http
        balance roundrobin
        option httpchk
        http-check send meth GET uri /index.html
        server s1 127.0.0.1:8081 check
        server s2 127.0.0.1:8082 check


listen web_tcp

        bind :1325

        server s1 127.0.0.1:8081 check inter 3s
        server s2 127.0.0.1:8082 check inter 3s


```

`При необходимости прикрепитe сюда скриншоты`
![установка 1](https://github.com/1985devops/gitlab-hw/blob/main/eee1.png)
![ссылка 1](https://github.com/1985devops/gitlab-hw/blob/main/haproxy1.cfg)
---

### Задание 2

1. `Запустил три simple python сервера на ubuntu на разных портах 8081,8082,8083`
2. `Настроил балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4`
3. `HAproxy балансирует только http-трафик, который адресован домену example.local`

```
global
        log /dev/log    local0
        log /dev/log    local1 notice
        chroot /var/lib/haproxy
        stats socket /run/haproxy/admin.sock mode 660 level admin expose-fd listeners
        stats timeout 30s
        user haproxy
        group haproxy
        daemon

        # Default SSL material locations
        ca-base /etc/ssl/certs
        crt-base /etc/ssl/private

        # See: https://ssl-config.mozilla.org/#server=haproxy&server-version=2.0.3&config=intermediate
        ssl-default-bind-ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM>
        ssl-default-bind-ciphersuites TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256
        ssl-default-bind-options ssl-min-ver TLSv1.2 no-tls-tickets

defaults
        log     global
        mode    http
        option  httplog
        option  dontlognull
        timeout connect 5000
        timeout client  50000
        timeout server  50000
        errorfile 400 /etc/haproxy/errors/400.http
        errorfile 403 /etc/haproxy/errors/403.http
        errorfile 408 /etc/haproxy/errors/408.http
        errorfile 500 /etc/haproxy/errors/500.http
        errorfile 502 /etc/haproxy/errors/502.http
        errorfile 503 /etc/haproxy/errors/503.http
        errorfile 504 /etc/haproxy/errors/504.http

listen stats  # веб-страница со статистикой
        bind                    :888
        mode                    http
        stats                   enable
        stats uri               /stats
        stats refresh           5s
        stats realm             Haproxy\ Statistics


listen web_tcp

frontend main_front
    bind *:8088
    # ACL: проверяем, что в заголовке Host указано example.local
    acl is_example_local hdr(host) -i example.local
    # Если условие верно, отправляем на бэкенд
    use_backend web_servers if is_example_local

backend web_servers
    mode http
    balance roundrobin
    server s1 127.0.0.1:8081 weight 2 check
    server s2 127.0.0.1:8082 weight 3 check
    server s3 127.0.0.1:8083 weight 4 check

```

`При необходимости прикрепитe сюда скриншоты`
![установка 2](https://github.com/1985devops/gitlab-hw/blob/main/eee2.png)
![установка 3](https://github.com/1985devops/gitlab-hw/blob/main/eee3.png)
![ссылка 2](https://github.com/1985devops/gitlab-hw/blob/main/haproxy2.cfg)


---

### Задание 3* со звёздочкой

1. `Настроил связку HAProxy + Nginx`
2. `Настроил Nginx так, чтобы файлы .jpg и .png выдавались самим Nginx, а остальные запросы переадресовывались на HAProxy, который в свою очередь переадресовывал их на два Simple Python server.`



```
upstream example_app {
    server 127.0.0.1:8081;
    server 127.0.0.1:8082;
    server 127.0.0.1:8083;
}

server {
    listen       80;
    server_name  example-http.com;

    access_log  /var/log/nginx/example-http.com-access.log;
    error_log   /var/log/nginx/example-http.com-error.log;

    location ~* \.(jpg|jpeg|png|gif)$ {
        root /var/www/images;
        try_files $uri =404;
    }

    location / {
        proxy_pass http://example_app;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}


```

```
user www-data;
worker_processes auto;
pid /run/nginx.pid;
error_log /var/log/nginx/error.log;
include /etc/nginx/modules-enabled/*.conf;

events {
        worker_connections 768;

}

http {

        sendfile on;
        tcp_nopush on;
        types_hash_max_size 2048;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
        ssl_prefer_server_ciphers on;

        access_log /var/log/nginx/access.log;

        gzip on;

        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}


```

`При необходимости прикрепитe сюда скриншоты`
![установка 4](https://github.com/1985devops/gitlab-hw/blob/main/eee4.png)
![установка 5](https://github.com/1985devops/gitlab-hw/blob/main/eee5.png)
![установка 6](https://github.com/1985devops/gitlab-hw/blob/main/eee6.png)
![установка 7](https://github.com/1985devops/gitlab-hw/blob/main/eee7.png)
![установка 8](https://github.com/1985devops/gitlab-hw/blob/main/eee8.png)
![ссылка 3](https://github.com/1985devops/gitlab-hw/blob/main/haproxy3.cfg)
![ссылка 4](https://github.com/1985devops/gitlab-hw/blob/main/nginx3.conf)

### Задание 4* со звёздочкой

1. ` `

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка 10](https://github.com/)

### Задание 5* со звёздочкой

1. ``

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка ](https://github.com/)

### Задание 6* со звёздочкой

1. ` `
2. ` `
2. ` `

```                                                  
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка ](https://)
![установка ](https://)

### Задание 7* со звёздочкой

1. ` `
2. ` `
2. ` `
3. ` `

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`

![установка ](https://)
![установка ](https://)

### Задание 8* со звёздочкой

1. ` `

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка ](https://)
![установка ](https://)
![установка ](https://)
![установка ](https://)

### Задание 9* со звёздочкой

1. ` `

```
Поле для вставки кода...

```


`При необходимости прикрепитe сюда скриншоты`

















