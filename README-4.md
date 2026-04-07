# Домашнее задание к занятию «Отказоустойчивость в облаке» -  Нугаев Алексей


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

1. `Создал группу из 2 виртуальных машин с балансировщиком нагрузки.`
2. `Nginx поставил так же автоматизированно.`

```
# 1. Находим существующую сеть по имени
data "yandex_vpc_network" "default" {
  name = "network-1"
}

# 2. Создаем подсеть в этой сети
resource "yandex_vpc_subnet" "subnet-1" {
  name           = "subnet-for-lb"
  zone           = "ru-central1-a"
  network_id     = data.yandex_vpc_network.default.id
  v4_cidr_blocks = ["192.168.50.0/24"]
}

# 3. Создаем 2 дешевых веб-сервера
resource "yandex_compute_instance" "vm" {
  count = 2
  name  = "web-server-${count.index + 1}"
  zone  = "ru-central1-a"

  resources {
    cores         = 2
    memory        = 2
    core_fraction = 20
  }

  scheduling_policy {
    preemptible = true
  }

  boot_disk {
    initialize_params {
      image_id = "fd80on0ma1ic60hees6n"
    }
  }

  network_interface {
    subnet_id = yandex_vpc_subnet.subnet-1.id
    nat       = true
  }

  metadata = {
    user-data = "#!/bin/bash\napt update && apt install -y nginx\nsystemctl start nginx"
    ssh-keys  = "ubuntu:${file("~/.ssh/id_rsa.pub")}"
  }
}

# 4. Создаем целевую группу
resource "yandex_lb_target_group" "tg" {
  name = "web-servers-tg"

  dynamic "target" {
    for_each = yandex_compute_instance.vm
    content {
      subnet_id = yandex_vpc_subnet.subnet-1.id
      address   = target.value.network_interface.0.ip_address
    }
  }
}

# 5. Создаем балансировщик
resource "yandex_lb_network_load_balancer" "lb" {
  name = "web-lb"

  listener {
    name = "http-listener"
    port = 80
    external_address_spec {
      ip_version = "ipv4"
    }
  }

  attached_target_group {
    target_group_id = yandex_lb_target_group.tg.id

    healthcheck {
      name = "http-check"
      http_options {
        port = 80
        path = "/"
      }
    }
  }
}


```

`При необходимости прикрепитe сюда скриншоты`
![установка 1](https://github.com/1985devops/gitlab-hw/blob/main/ggg1.png)
![установка 2](https://github.com/1985devops/gitlab-hw/blob/main/ggg2.png)
![установка 3](https://github.com/1985devops/gitlab-hw/blob/main/ggg3.png)
![установка 4](https://github.com/1985devops/gitlab-hw/blob/main/ggg4.png)
![установка 5](https://github.com/1985devops/gitlab-hw/blob/main/ggg5.png)
![установка 6](https://github.com/1985devops/gitlab-hw/blob/main/ggg6.png)
![установка 7](https://github.com/1985devops/gitlab-hw/blob/main/ggg7.png)

---

### Задание 2

1. ` `
2. ` `
3. ` `

```

```

`При необходимости прикрепитe сюда скриншоты`
![установка ](https://github.com/1985devops/gitlab-hw/blob/main/.png)
![установка ](https://github.com/1985devops/gitlab-hw/blob/main/.png)

---

### Задание

1. ` `
2. ` `

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка ](https://github.com/1985devops/gitlab-hw/blob/main/.png)
![установка ](https://github.com/1985devops/gitlab-hw/blob/main/.png)

### Задание 

1. ``

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка ](https://github.com/)

### Задание 

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

















