# Домашнее задание к занятию 4 «Оркестрация группой Docker контейнеров на примере Docker Compose»` - Мельник Юрий Александрович


## Задача 1

Сценарий выполнения задачи:
- Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
- Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: ```{"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}```
- Зарегистрируйтесь и создайте публичный репозиторий  с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
- скачайте образ nginx:1.21.1;
- Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
```
- Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП). 
- Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .

## Решение 1
в папке 

```sh
docker pull nginx:1.21.1
```

```sh
docker build -t custom-nginx:1.0.0 .
```

```sh
docker tag custom-nginx:1.0.0 ysatii/custom-nginx:1.0.0
```

```sh
docker push ysatii/custom-nginx:1.0.0
```

https://hub.docker.com/repository/docker/ysatii/custom-nginx/general

https://hub.docker.com/repository/docker/ysatii/custom-nginx/tags/1.0.0/sha256-d0323f74b6af50bb16313c3d751152f61a9d81d2a6faae8cdda9d632db0dab91  

ссылка на [Dockerfile ](https://github.com/ysatii/hw4-docker/tree/main/1)

## Задача 2
1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080
2. Не удаляя, переименуйте контейнер в "custom-nginx-t2"
3. Выполните команду ```date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html```
4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

# Ответ 2
```sh
docker run -d --name "melnik-ua-nginx-t2" -p 127.0.0.1:8080:80 custom-nginx:1.0.0
docker rename melnik-ua-nginx-t2 custom-nginx-t2
```

![Скриншот 1](https://github.com/ysatii/hw4-docker/blob/main/img/docker1.jpg)  
![Скриншот 2](https://github.com/ysatii/hw4-docker/blob/main/img/docker2.jpg) 
![Скриншот 3](https://github.com/ysatii/hw4-docker/blob/main/img/docker3.jpg) 
![Скриншот 4](https://github.com/ysatii/hw4-docker/blob/main/img/docker4.jpg) 

## Задача 3
1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
3. Выполните ```docker ps -a``` и объясните своими словами почему контейнер остановился.
4. Перезапустите контейнер
5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
8. Запомните(!) и выполните команду ```nginx -s reload```, а затем внутри контейнера ```curl http://127.0.0.1:80 ; curl http://127.0.0.1:81```.
9. Выйдите из контейнера, набрав в консоли  ```exit``` или Ctrl-D.
10. Проверьте вывод команд: ```ss -tlpn | grep 127.0.0.1:8080``` , ```docker port custom-nginx-t2```, ```curl http://127.0.0.1:8080```. Кратко объясните суть возникшей проблемы.
11. * Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. [пример источника](https://www.baeldung.com/linux/assign-port-docker-container)
12. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

# ответ 3
![Скриншот 5](https://github.com/ysatii/hw4-docker/blob/main/img/docker5.jpg) 
Комбинация Ctrl-C передает контейнеру сигнал SIGINT, тем самым завершает его основной процесс и контейнер останавливается.  

установим  nano 
![Скриншот 6](https://github.com/ysatii/hw4-docker/blob/main/img/docker6.jpg) 

изменим порт на 81 
![Скриншот 7](https://github.com/ysatii/hw4-docker/blob/main/img/docker7.jpg) 
![Скриншот 8](https://github.com/ysatii/hw4-docker/blob/main/img/docker8.jpg) 
![Скриншот 9](https://github.com/ysatii/hw4-docker/blob/main/img/docker9.jpg) 

контейнер по прежнему ведет проброс трафика на внутренний 80 порт! но он перестал отвечать. дальнейная работа не возможна нет порта который отвечает на веб запросы

удаляем не останавливая
```sh
docker rm -f custom-nginx-t2
```

## Задача 4


- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку  текущий рабочий каталог ```$(pwd)``` на хостовой машине в ```/data``` контейнера, используя ключ -v.
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив текущий рабочий каталог ```$(pwd)``` в ```/data``` контейнера. 
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.
- Добавьте ещё один файл в текущий каталог ```$(pwd)``` на хостовой машине.
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.


В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

# ответ 4
заппускаем два контейнера и проверяем что они в работе
![Скриншот 10](https://github.com/ysatii/hw4-docker/blob/main/img/docker10.jpg) 

```sh
docker run -d   --name centos-container   -v "$(pwd):/data"   centos tail -f /dev/null
docker run -d   --name debian-container   -v "$(pwd):/data"   debian tail -f /dev/null
docker ps 
```
поключимся к первому контейнеру и создадим файл, проверим что он создался 
```sh
docker exec -it centos-container bash
echo "Hello from CentOS container" > /data/file_in_container.txt
ls /data
cat /data/file_in_container.txt
```
Выйдем  из контейнера командой exit.

Создание файла на хостовой машине
```sh
 echo "Hello from host" > "$(pwd)/file_on_host.txt"
ls "$(pwd)"
cat "$(pwd)/file_on_host.txt"
 ```

Просмотр файлов во втором контейнере
```sh
docker exec -it debian-container bash
ls /data
```
![Скриншот 11](https://github.com/ysatii/hw4-docker/blob/main/img/docker11.jpg) 


## Задача 5

1. Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него.
"compose.yaml" с содержимым:
```
version: "3"
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
"docker-compose.yaml" с содержимым:
```
version: "3"
services:
  registry:
    image: registry:2

    ports:
    - "5000:5000"
```

И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )

2. Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)

3. Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/
4. Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)
5. Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local  окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:

```
version: '3'

services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"
```
6. Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".

7. Удалите любой из манифестов компоуза(например compose.yaml).  Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод, файл compose.yaml , скриншот portainer c задеплоенным компоузом.

# ответ 5
1. По умолчанию путь к файлу Compose: compose.yaml (предпочтительный) или compose.yml. Compose также поддерживает docker-compose.yaml и docker-compose.yml для обеспечения обратной совместимости с более ранними версиями. Если в рабочем каталоге оба файла, Compose предпочитает compose.yaml.

![Скриншот 12](https://github.com/ysatii/hw4-docker/blob/main/img/docker12.jpg) 

2. Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла

```
version: "3"

include:
  - docker-compose.yaml

services:
  portainer:
    image: portainer/portainer-ce:latest
    network_mode: host
    ports:
      - "9000:9000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
![Скриншот 13](https://github.com/ysatii/hw4-docker/blob/main/img/docker13.jpg) 
