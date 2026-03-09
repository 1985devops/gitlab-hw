# Домашнее задание к занятию «Система мониторинга Zabbix» - Нугаев Алексей


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

1. `Установил на яндекс облаке виртуальную машину с debian 12. Поставил PostgreSQL.`
2. `Пользуясь конфигуратором команд с официального сайта, установил 7.0 LTS версию Zabbix с поддержкой PostgreSQL и Apache.`
3. `Выполнил установки Zabbix Server и Zabbix Web Server.`
```
Поле для вставки кода...

# wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.0+debian12_all.deb
# dpkg -i zabbix-release_latest_7.0+debian12_all.deb
# apt update

# apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent

# sudo -u postgres createuser --pwprompt zabbix
# sudo -u postgres createdb -O zabbix zabbix

# zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

# systemctl restart zabbix-server zabbix-agent apache2
# systemctl enable zabbix-server zabbix-agent apache2

```

`При необходимости прикрепитe сюда скриншоты`
![установка 1](https://github.com/1985devops/gitlab-hw/blob/main/aaa.jpg)
![установка 2](https://github.com/1985devops/gitlab-hw/blob/main/bbb.jpg)
![установка 3](https://github.com/1985devops/gitlab-hw/blob/main/ccc.jpg)
![установка 4](https://github.com/1985devops/gitlab-hw/blob/main/ddd.jpg)

---

### Задание 2

1. `Установил Zabbix Agent на 2 вирт.машины, zabbix-agent1 и zabbix-agent2.`
2. `Добавил Zabbix Server в список разрешенных серверов Zabbix Agentов.`
3. `Добавил Zabbix Agentов в раздел Configuration > Hosts Zabbix Servera.`
4. `Проверил, в Latest Data начали появляться данные с добавленных агентов.`

```
Поле для вставки кода...

# wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.0+debian12_all.deb
# dpkg -i zabbix-release_latest_7.0+debian12_all.deb
# apt update

# apt install zabbix-agent

# systemctl restart zabbix-agent
# systemctl enable zabbix-agent

```

`При необходимости прикрепитe сюда скриншоты`
![установка 5](https://github.com/1985devops/gitlab-hw/blob/main/eee.jpg)
![установка 6](https://github.com/1985devops/gitlab-hw/blob/main/fff.jpg)
![установка 7](https://github.com/1985devops/gitlab-hw/blob/main/ggg.jpg)
![установка 8](https://github.com/1985devops/gitlab-hw/blob/main/hhh.jpg)
![установка 9](https://github.com/1985devops/gitlab-hw/blob/main/iii.jpg)
![установка 10](https://github.com/1985devops/gitlab-hw/blob/main/jjj.jpg)

---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Установил Zabbix Agent на Windows (компьютер) домашний за яндекс cloud и подключил его к серверу Zabbix.`

```
Поле для вставки кода...


```

`При необходимости прикрепитe сюда скриншоты`
![установка 11](https://github.com/1985devops/gitlab-hw/blob/main/kkk.jpg)
![установка 12](https://github.com/1985devops/gitlab-hw/blob/main/lll.jpg)
![установка 13](https://github.com/1985devops/gitlab-hw/blob/main/mmm.jpg)


### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
