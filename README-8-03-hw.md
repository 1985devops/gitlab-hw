# Домашнее задание к занятию «GitLab» - Нугаев Алексей


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

1. `Установил на virtual box ubuntu образ GitLab локально, используя Vagrantfile`
2. `Создал новый проект и пустой репозиторий в нём. Зарегистрировал gitlab-runner для этого проекта и запуститл его в режиме Docker`

```
Поле для вставки кода...

# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu64/noble64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.56.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  config.vm.disk :disk, size: "15GB", primary: true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
    vb.memory = "6144"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get update
    # install docker & docker-compose
    apt-get install -y docker.io docker-compose
    # install gitlab: https://about.gitlab.com/install/#ubuntu
    apt-get install -y curl openssh-server ca-certificates tzdata perl
    curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
    sudo EXTERNAL_URL="http://gitlab.localdomain" apt-get install gitlab-ee
    # pull some images in advance
    docker pull gitlab/gitlab-runner:latest
    docker pull sonarsource/sonar-scanner-cli:latest
    docker pull golang:1.17
    docker pull docker:latest
    # set sysctl for sonarqube
    sysctl vm.max_map_count=262144
    # run sonarqube
    # cd /vagrant && docker-compose up -d
    # add some records to /etc/hosts
    echo -e "192.168.56.10\tubuntu-bionic\tubuntu-bionic" >> /etc/hosts
    echo -e "192.168.56.10\tgitlab.localdomain\tgitlab" >> /etc/hosts
  SHELL
end


```

`При необходимости прикрепитe сюда скриншоты`
![установка 1 ](https://github.com/1985devops/gitlab-hw/blob/main/11111.jpg)
![установка 2](https://github.com/1985devops/gitlab-hw/blob/main/22222.jpg)
![установка 3](https://github.com/1985devops/gitlab-hw/blob/main/33333.jpg)
![установка 4](https://github.com/1985devops/gitlab-hw/blob/main/44444.jpg)
![установка 5](https://github.com/1985devops/gitlab-hw/blob/main/55555.jpg)
![установка 6](https://github.com/1985devops/gitlab-hw/blob/main/66666.jpg)
![установка 7](https://github.com/1985devops/gitlab-hw/blob/main/77777.jpg)

---

### Задание 2

1. `Запушьтел репозиторий на GitLab, изменив origin.`
2. `Создал .gitlab-ci.yml`

```
Поле для вставки кода...

stages:
  - test

hello_job:
  stage: test
  image: golang:1.17
  script:
    - go version
    - echo "Hello! GitLab Runner is working correctly."

```

`При необходимости прикрепитe сюда скриншоты`
![установка 8](https://github.com/1985devops/gitlab-hw/blob/main/88888.jpg)
![установка 9](https://github.com/1985devops/gitlab-hw/blob/main/99999.jpg)
![установка 10](https://github.com/1985devops/gitlab-hw/blob/main/10111.jpg)
![установка 11](https://github.com/1985devops/gitlab-hw/blob/main/10222.jpg)
![установка 12](https://github.com/1985devops/gitlab-hw/blob/main/10333.jpg)
![установка 12](https://github.com/1985devops/gitlab-hw/blob/main/10444.jpg)
![установка 12](https://github.com/1985devops/gitlab-hw/blob/main/10555.jpg)


---

### Задание 3

`Приведите ответ в свободной форме........`

1. ` `
2. ` `
3. ` `

```
Поле для вставки кода...


```

`При необходимости прикрепитe сюда скриншоты`
![ ]( )
![ ]( )

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
