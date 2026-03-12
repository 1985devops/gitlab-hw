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

1. `В веб-интерфейсе Zabbix Servera в разделе Templates создал новый шаблон "Custom Hardware Monitor netology"`
2. `Создал Item "CPU load" который собирает информацию об загрузке CPU в процентах`
3. `Создал Item "RAM load" который собирает информацию об загрузке RAM в процентах`

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка 1](https://github.com/1985devops/gitlab-hw/blob/main/aaa3.jpg)
![установка 2](https://github.com/1985devops/gitlab-hw/blob/main/aaa4.jpg)
![установка 3](https://github.com/1985devops/gitlab-hw/blob/main/aaa5.jpg)

---

### Задание 2

1. `Установил Zabbix Agent на 2 вирт.машины, zabbix-agent1 и zabbix-agent2.`
2. `Добавил Zabbix Server в список разрешенных серверов Zabbix Agentов.`
3. `Добавил Zabbix Agentов в раздел Configuration > Hosts Zabbix Servera.`
4. `Прикрепил за каждым хостом шаблон Linux by Zabbix Agent`
5. `Проверил, в Latest Data начали появляться данные с добавленных агентов.`

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка 4](https://github.com/1985devops/gitlab-hw/blob/main/aaa1.jpg)
![установка 5](https://github.com/1985devops/gitlab-hw/blob/main/aaa2.jpg)

---

### Задание 3

1. `Зашел в настройки каждого хоста и в разделе Templates и прикрепил к этому хосту ваш шаблон`
2. `К каждому хосту привяжите шаблон Linux by Zabbix Agent`
3. `Latest Data начали поступать необходимые данные из шаблона`

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка 6](https://github.com/1985devops/gitlab-hw/blob/main/aaa6.jpg)

### Задание 4

1. `В разделе Dashboards создл дашборд  Load average (1m avg) и Memory utilization`
2. `Разместите на нём два графика`

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка 7](https://github.com/1985devops/gitlab-hw/blob/main/aaa7.jpg)
![установка 8](https://github.com/1985devops/gitlab-hw/blob/main/aaa8.jpg)

### Задание 5* со звёздочкой

1. `Привязал к линку триггер, agent.ping хоста nugaevav-1 host, установиk индикатор сработавшего триггера красную пунктирную линию`
2. `Выключил хост, nugaevav-1 host. Дождался срабатывания триггера.`

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка 9](https://github.com/1985devops/gitlab-hw/blob/main/aaa9.jpg)
![установка 10](https://github.com/1985devops/gitlab-hw/blob/main/aaa10.jpg)

### Задание 6* со звёздочкой

1. `Создал UserParameter на bash и прикрепил его к шаблону Custom Hardware Monitor netology.`
2. `Вызывает скрипт, который при получении 1 будет возвращать ФИО Нугаев Алексей Валерьевич`
2. `при получении 2 возвращает текущую дату`

```                                                  
#!/bin/bash
if [ "$1" == "1" ]; then
    echo "Нугаев Алексей Валерьевич"
elif [ "$1" == "2" ]; then
    date +%Y-%m-%d
else
    echo "Ошибка: используйте 1 или 2"
fi

```

`При необходимости прикрепитe сюда скриншоты`
![установка 11](https://github.com/1985devops/gitlab-hw/blob/main/aaa11.jpg)
![установка 12](https://github.com/1985devops/gitlab-hw/blob/main/aaa12.jpg)

### Задание 7* со звёздочкой

1. `Доработал Python-скрипт из лекции, создал UserParameter и прикрепил его к своему шаблону. `
2. `при получении 1 возвращает Нугаев Алексей Валерьевич`
2. `при получении 2 возвращает текущую дату`
3. `делает всё из лекции`

```
import sys
import os
import re
from datetime import date

# Проверяем, передан ли хотя бы один аргумент
if len(sys.argv) < 2:
    print("Error: No arguments provided")
    sys.exit(1)

arg = sys.argv[1]

# Новая логика задания 7
if arg == '1':
    print("Твои Фамилия Имя Отчество") # <-- Впиши здесь свои данные
elif arg == '2':
    print(date.today())

# Оригинальная логика из лекции
elif arg == '-ping':
    # Тут нужен второй аргумент (IP), поэтому проверяем sys.argv[2]
    result = os.popen("ping -c 1 " + sys.argv[2]).read()
    res = re.findall(r"time=(.*) ms", result)
    if res:
        print(res[0])
    else:
        print("0")
elif arg == '-simple_print':
    print(sys.argv[2])
else:
    print(f"unknown input: {arg}")

```

`При необходимости прикрепитe сюда скриншоты`
![установка 13](https://github.com/1985devops/gitlab-hw/blob/main/aaa13.jpg)
![установка 14](https://github.com/1985devops/gitlab-hw/blob/main/aaa14.jpg)

### Задание 8* со звёздочкой

1. `Настроил автообнаружение и прикрепил к хостам шаблона.`

```
Поле для вставки кода...

```

`При необходимости прикрепитe сюда скриншоты`
![установка 15](https://github.com/1985devops/gitlab-hw/blob/main/aaa15.jpg)
![установка 16](https://github.com/1985devops/gitlab-hw/blob/main/aaa16.jpg)
![установка 17](https://github.com/1985devops/gitlab-hw/blob/main/aaa17.jpg)
![установка 18](https://github.com/1985devops/gitlab-hw/blob/main/aaa18.jpg)

### Задание 9* со звёздочкой

1. `Ниже скрипты Vagrant для 2-х агентов в яндекс облаке, имеют автообнаружению сервером, а так же остальные параметры пользователей.`

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

# Массив ваших виртуалок в Яндекс.Облаке
virt_machines=[
  { :hostname => "zabbix-agent1", :ip => "10.130.0.13" },
  { :hostname => "zabbix-agent2", :ip => "10.130.0.28" }
]

# Общие параметры
HOST_MEMMORY = "2048" 
HOST_CPUS = 2
HOST_VM_BOX = "bento/ubuntu-20.04"
ZABBIX_SERVER_IP = '10.130.0.32' # Ваш реальный IP сервера

Vagrant.configure("2") do |config|
  virt_machines.each do |machine|
    config.vm.box = HOST_VM_BOX
    config.vm.define machine[:hostname] do |node|
      node.vm.hostname = machine[:hostname]
      node.vm.network "private_network", ip: machine[:ip]
      
      node.vm.provider "virtualbox" do |vb|
        vb.memory = HOST_MEMMORY
        vb.cpus = HOST_CPUS
      end

      # Передаем аргументы в скрипт: имя хоста, IP агента и IP сервера
      node.vm.provision "shell", path: "zabbix-agent.sh", 
        args: [machine[:hostname], machine[:ip], ZABBIX_SERVER_IP]
    end
  end
end

```

```
#!/bin/bash

# Считываем аргументы из Vagrantfile
HOSTNAME=$1
MY_IP=$2
ZABBIX_SERVER=$3

# 1. Установка компонентов
sudo apt-get update
sudo apt-get install -y zabbix-agent python3

# 2. Создание Python-скрипта (Задание 7)
sudo mkdir -p /etc/zabbix/scripts
cat <<EOF | sudo tee /etc/zabbix/scripts/hw_script.py
import sys
import os
import re
from datetime import date

if len(sys.argv) < 2: sys.exit(1)
arg = sys.argv

if arg == '1':
    print("Нугаев Алексей Валерьевич")
elif arg == '2':
    print(date.today())
elif arg == '-ping':
    result = os.popen("ping -c 1 " + sys.argv).read()
    res = re.findall(r"time=(.*) ms", result)
    print(res if res else "0")
else:
    print(f"unknown input: {arg}")
EOF
sudo chmod +x /etc/zabbix/scripts/hw_script.py

# 3. Настройка UserParameter и конфига агента
echo "UserParameter=custom.py[*],/usr/bin/python3 /etc/zabbix/scripts/hw_script.py \$1 \$2" | sudo tee /etc/zabbix/zabbix_agentd.d/userparams.conf

sudo sed -i "s/Server=127.0.0.1/Server=$ZABBIX_SERVER/g" /etc/zabbix/zabbix_agentd.conf
sudo sed -i "s/ServerActive=127.0.0.1/ServerActive=$ZABBIX_SERVER/g" /etc/zabbix/zabbix_agentd.conf
sudo sed -i "s/Hostname=Zabbix server/Hostname=$HOSTNAME/g" /etc/zabbix/zabbix_agentd.conf

# 4. Перезапуск для применения настроек
sudo systemctl restart zabbix-agent


```

`При необходимости прикрепитe сюда скриншоты`


