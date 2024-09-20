# Домашнее задание к занятию "Что такое DevOps" - `Каргапольцев Константин Сергеевич`


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

Что нужно сделать:

    Установите себе jenkins по инструкции из лекции или любым другим способом из официальной документации. Использовать Docker в этом задании нежелательно.
    Установите на машину с jenkins golang.
    Используя свой аккаунт на GitHub, сделайте себе форк репозитория. В этом же репозитории находится дополнительный материал для выполнения ДЗ.
    Создайте в jenkins Freestyle Project, подключите получившийся репозиторий к нему и произведите запуск тестов и сборку проекта go test . и docker build ..

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

Решение1

    - Устанавливаем Java: 
sudo apt-get install default-jre

    - Устанавливаем Jenkins:
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
    https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins

    - Устанавливаем golang:
wget https://go.dev/dl/go1.17.5.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.17.5.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> /etc/profile

  - Добавлям пользователя Jenkins в группу Docker
sudo usermod -aG docker jenkins

- Заходим в Jenkins (192.168.123.4:8080):
Пароль берем из папки: 
/var/lib/jenkins/secrets/initialAdminPassword

![Настройки 1.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/Настройки%201.png)
![Настройки 1-2.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/Настройки%201-2.png)
![Вывод консоли 1.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/Вывод%20консоли%201.png)
![Вывод консоли 2.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/Вывод%20консоли%202.png)
![Результат сборки.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/Результат%20сборки.png)

---

### Задание 2

Что нужно сделать:
Создайте новый проект pipeline.
Перепишите сборку из задания 1 на declarative в виде кода.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

Решение 2:

![Настройки 2.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/Настройки%202.png)
![Решение консоль.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/Решение%202%20консоль.png)

---

### Задание 3

Что нужно сделать:

    Установите на машину Nexus.
    Создайте raw-hosted репозиторий.
    Измените pipeline так, чтобы вместо Docker-образа собирался бинарный go-файл. Команду можно скопировать из Dockerfile.
    Загрузите файл в репозиторий с помощью jenkins.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

Решение 3:

- Установил Nexus:
docker run -d -p 8081:8081 -p 8082:8082 --name nexus -e INSTALL4J_ADD_VM_PARAMS="-Xms512m -Xmx512m -XX:MaxDirectMemorySize=273m" sonatype/nexus3
- Зашел в Nexus - 192.168.123.4.8081
- Создайте raw-hosted репозиторий - kks_rawhosted
- Переписал pipline из первого задания
- Загрузить файл в репозиторий при помощи Jenkins:
sh 'curl -u admin:2k1a3r8a34
http://192.168.123.4:8081/repository/kks_rawhosted/ --upload-file  ubuntu-bionic:8082/hello-world.tgz -v'


![репозиторий.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/репозитори.png)
![pipeline.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/pipeline.png)
![Консоль.png](https://github.com/KargapoltcevKS/CI-CD-DewOps/blob/main/img/Консоль.png) 

---
