# Домашнее задание к занятию "Что такое DevOps. CI/CD" - Нугаев Алексей


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

1. `Установил на virtual box ubuntu программу jenkins and goland`
2. `Сделал форк репозитория netology-code/sdvps-materials на свой 1985devops`
3. `Создал в jenkins Freestyle Project, подключил репозиторий https://github.com/1985devops/sdvps-materials.git`
4. `Запустил тесты и сборку проекта go test . и docker build`

```
Поле для вставки кода...

Started by user Nugaev Aleksey

Running as SYSTEM
Building in workspace /var/lib/jenkins/workspace/gitlab-hw-build
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/gitlab-hw-build/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/1985devops/sdvps-materials.git # timeout=10
Fetching upstream changes from https://github.com/1985devops/sdvps-materials.git
 > git --version # timeout=10
 > git --version # 'git version 2.43.0'
 > git fetch --tags --force --progress -- https://github.com/1985devops/sdvps-materials.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision 223dbc3f489784448004e020f2ef224f17a7b06d (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
Commit message: "Update README.md"
 > git rev-list --no-walk 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
[gitlab-hw-build] $ /bin/sh -xe /tmp/jenkins17688033726439233999.sh
+ /usr/local/go/bin/go test ./...
ok  	github.com/netology-code/sdvps-materials	(cached)
+ docker build -t localhost:8082/hello-world:v5 .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon    254kB

Step 1/8 : FROM golang:1.16 AS builder
 ---> 972d8c0bc0fc
Step 2/8 : WORKDIR $GOPATH/src/github.com/netology-code/sdvps-materials
 ---> Using cache
 ---> 3ac4d9f85665
Step 3/8 : COPY . ./
 ---> Using cache
 ---> fa8721d9d589
Step 4/8 : RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o /app .
 ---> Using cache
 ---> ad34ccfb619f
Step 5/8 : FROM alpine:latest
 ---> a40c03cbb81c
Step 6/8 : RUN apk -U add ca-certificates
 ---> Using cache
 ---> 60a0fecbbb9f
Step 7/8 : COPY --from=builder /app /app
 ---> Using cache
 ---> 82e1b86ccfed
Step 8/8 : CMD ["/app"]
 ---> Using cache
 ---> fec52bf753f2
Successfully built fec52bf753f2
Successfully tagged localhost:8082/hello-world:v5
+ docker login localhost:8082 -u admin -p admin
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
Login Succeeded
+ docker push localhost:8082/hello-world:v5
The push refers to repository [localhost:8082/hello-world]
efad79c1bc85: Preparing
e961eb23e0b3: Preparing
989e799e6349: Preparing
efad79c1bc85: Pushed
e961eb23e0b3: Pushed
989e799e6349: Pushed
v5: digest: sha256:dbdd829e7e2f7fedffb3724876e59cc3cdf5dddc78bf517da60b1461ba0f013d size: 950
+ docker logout localhost:8082
Removing login credentials for localhost:8082
Finished: SUCCESS


```

`При необходимости прикрепитe сюда скриншоты`
![код запуска сборки](https://github.com/1985devops/gitlab-hw/blob/main/Screenshot_2.jpg)
![запуск сборки](https://github.com/1985devops/gitlab-hw/blob/main/Screenshot_1.jpg)

---

### Задание 2

1. `Создал новый проект pipeline`
2. `Переписал сборку из задания 1 на declarative в виде кода`

```
Поле для вставки кода...

Started by user Nugaev Aleksey

[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins
 in /var/lib/jenkins/workspace/gitlab-hw-pipeline
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Git)
[Pipeline] git
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/gitlab-hw-pipeline/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/1985devops/sdvps-materials.git # timeout=10
Fetching upstream changes from https://github.com/1985devops/sdvps-materials.git
 > git --version # timeout=10
 > git --version # 'git version 2.43.0'
 > git fetch --tags --force --progress -- https://github.com/1985devops/sdvps-materials.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision 223dbc3f489784448004e020f2ef224f17a7b06d (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
 > git branch -a -v --no-abbrev # timeout=10
 > git checkout -b main 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
Commit message: "Update README.md"
First time build. Skipping changelog.
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Test)
[Pipeline] sh
+ /usr/local/go/bin/go test ./...
ok  	github.com/netology-code/sdvps-materials	0.007s
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Build)
[Pipeline] sh
+ docker build . -t localhost:8082/hello-world:v3
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon  256.5kB

Step 1/8 : FROM golang:1.16 AS builder
 ---> 972d8c0bc0fc
Step 2/8 : WORKDIR $GOPATH/src/github.com/netology-code/sdvps-materials
 ---> Using cache
 ---> 3ac4d9f85665
Step 3/8 : COPY . ./
 ---> f904dca22a04
Step 4/8 : RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o /app .
 ---> Running in fb612b831b6b
 ---> Removed intermediate container fb612b831b6b
 ---> fab565451e58
Step 5/8 : FROM alpine:latest
 ---> a40c03cbb81c
Step 6/8 : RUN apk -U add ca-certificates
 ---> Using cache
 ---> 60a0fecbbb9f
Step 7/8 : COPY --from=builder /app /app
 ---> Using cache
 ---> 82e1b86ccfed
Step 8/8 : CMD ["/app"]
 ---> Using cache
 ---> fec52bf753f2
Successfully built fec52bf753f2
Successfully tagged localhost:8082/hello-world:v3
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Push)
[Pipeline] sh
+ docker login localhost:8082 -u admin -p admin
WARNING! Using --password via the CLI is insecure. Use --password-stdin.

WARNING! Your credentials are stored unencrypted in '/var/lib/jenkins/.docker/config.json'.
Configure a credential helper to remove this warning. See
https://docs.docker.com/go/credential-store/

Login Succeeded
+ docker push localhost:8082/hello-world:v3
The push refers to repository [localhost:8082/hello-world]
efad79c1bc85: Preparing
e961eb23e0b3: Preparing
989e799e6349: Preparing
989e799e6349: Layer already exists
e961eb23e0b3: Layer already exists
efad79c1bc85: Layer already exists
v3: digest: sha256:dbdd829e7e2f7fedffb3724876e59cc3cdf5dddc78bf517da60b1461ba0f013d size: 950
+ docker logout localhost:8082
Removing login credentials for localhost:8082
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS


```

`При необходимости прикрепитe сюда скриншоты`
![сборка проект pipeline](https://github.com/1985devops/gitlab-hw/blob/main/Screenshot_3.jpg)
![код проект pipeline](https://github.com/1985devops/gitlab-hw/blob/main/Screenshot_4.jpg)

---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...

Started by user Nugaev Aleksey

[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins
 in /var/lib/jenkins/workspace/gitlab-hw-pipeline
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Git)
[Pipeline] git
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/gitlab-hw-pipeline/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/1985devops/sdvps-materials.git # timeout=10
Fetching upstream changes from https://github.com/1985devops/sdvps-materials.git
 > git --version # timeout=10
 > git --version # 'git version 2.43.0'
 > git fetch --tags --force --progress -- https://github.com/1985devops/sdvps-materials.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision 223dbc3f489784448004e020f2ef224f17a7b06d (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
 > git branch -a -v --no-abbrev # timeout=10
 > git branch -D main # timeout=10
 > git checkout -b main 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
Commit message: "Update README.md"
 > git rev-list --no-walk 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Test)
[Pipeline] sh
+ /usr/local/go/bin/go test ./...
ok  	github.com/netology-code/sdvps-materials	(cached)
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Build Binary)
[Pipeline] sh
+ CGO_ENABLED=0 GOOS=linux /usr/local/go/bin/go build -a -installsuffix nocgo -o myapp .
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Push to Nexus)
[Pipeline] sh
+ curl -v -u admin:admin123 --upload-file myapp http://localhost:8081/repository/my-raw-repo/myapp-v4
* Host localhost:8081 was resolved.
* IPv6: ::1
* IPv4: 127.0.0.1
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed

  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying [::1]:8081...
* Connected to localhost (::1) port 8081
* Server auth using Basic with user 'admin'
> PUT /repository/my-raw-repo/myapp-v4 HTTP/1.1
> Host: localhost:8081
> Authorization: Basic YWRtaW46YWRtaW4xMjM=
> User-Agent: curl/8.5.0
> Accept: */*
> Content-Length: 2497777
> Expect: 100-continue
> 
< HTTP/1.1 100 Continue
} [65536 bytes data]
* We are completely uploaded and fine
< HTTP/1.1 201 Created
< Server: Nexus/3.89.1-02 (COMMUNITY)
< X-Content-Type-Options: nosniff
< Content-Security-Policy: sandbox allow-forms allow-modals allow-popups allow-presentation allow-scripts allow-top-navigation
< X-XSS-Protection: 0
< Content-Length: 0
< 

100 2439k    0     0  100 2439k      0  7868k --:--:-- --:--:-- --:--:-- 7893k
* Connection #0 to host localhost left intact
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS


```

`При необходимости прикрепитe сюда скриншоты`
![сборка Nexus](https://github.com/1985devops/gitlab-hw/blob/main/Screenshot_6.jpg)
![репозиторий Nexus](https://github.com/1985devops/gitlab-hw/blob/main/Screenshot_5.jpg)

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
