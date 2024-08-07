# Домашнее задание к занятию 4 «Оркестрация группой Docker контейнеров на примере Docker Compose» Макаров Денис

### Инструкция к выполению

1. Для выполнения заданий обязательно ознакомьтесь с [инструкцией](https://github.com/netology-code/devops-materials/blob/master/cloudwork.MD) по экономии облачных ресурсов. Это нужно, чтобы не расходовать средства, полученные в результате использования промокода.
2. Практические задачи выполняйте на личной рабочей станции или созданной вами ранее ВМ в облаке.
3. Своё решение к задачам оформите в вашем GitHub репозитории в формате markdown!!!
4. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

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

Решение:

"https://hub.docker.com/repository/docker/dimakarov/custom-nginx/general"

![docker-hub](https://github.com/user-attachments/assets/74cf5b92-a49a-4882-b1de-d56780ed305d)

## Задача 2
1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080
2. Переименуйте контейнер в "custom-nginx-t2"
3. Выполните команду ```date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html```
4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

Решение:

Представлено на скриншотах ниже:

![pereimenovanie](https://github.com/user-attachments/assets/f2bfce8b-515b-4864-992f-0347c7524d87)

![Проверка работы2](https://github.com/user-attachments/assets/7e50c006-f894-4cb6-b0b6-6686d0d1a782)

![Проверка работы3](https://github.com/user-attachments/assets/9a9be93c-8dd8-449c-a57e-91de27e85ab5)



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

Решение:

Представлены скриншоты ниже:

![docker-attach](https://github.com/user-attachments/assets/f9d1a735-e2ae-44eb-8cc7-7fc18d967cde)

Контейнер завершил свою работу, т.к. на вход контейнера был послан сигнал ctrl-c.

![Снимок](https://github.com/user-attachments/assets/cd75be13-ed3b-4031-92bc-6ac0809ea71f)

![Проверка работы4](https://github.com/user-attachments/assets/d07c008d-b835-47a7-9943-253b54d8c95f)

![Проверка работы5](https://github.com/user-attachments/assets/c2f0576d-a646-4ac6-8123-a571f56f4e16)

Внутри контейнера мы перенастроили NGINX слушать не порт 80 а слушать теперь порт 81. А в настройках докер осталось что докер пересылает со внешнего порта 8080 на порт контейнера 80 - а там никто не слушает этот порт. Поэтому нет ответа.

![Проверка работы6](https://github.com/user-attachments/assets/fdbec35b-91a3-4717-b00d-f3712cd8d7ec)



## Задача 4

- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку  текущий рабочий каталог ```$(pwd)``` на хостовой машине в ```/data``` контейнера, используя ключ -v.
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив текущий рабочий каталог ```$(pwd)``` в ```/data``` контейнера. 
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.
- Добавьте ещё один файл в текущий каталог ```$(pwd)``` на хостовой машине.
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.


В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

Решение:

Выполненные команды представлены на скриншотах ниже:

![4-1 zadanie](https://github.com/user-attachments/assets/e91c05ec-a7dc-402b-98a8-242d9663ed7e)

![4-2 zadanie](https://github.com/user-attachments/assets/10244afc-120f-41c4-a466-8a70af37b734)

![4-3 zadanie](https://github.com/user-attachments/assets/14175f2a-0ed7-44e9-b19f-16141952ff7c)

![4-4 zadanie](https://github.com/user-attachments/assets/c8c52517-e072-484e-9dfe-e220f4e739fc)

![zadanie 4-5](https://github.com/user-attachments/assets/ba7565a2-59e0-418b-a365-e0cf788efa10)


## Задача 5

1. Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него.
"compose.yaml" с содержимым:
```
version: "3"
services:
  portainer:
    image: portainer/portainer-ce:latest
    network_mode: host
    ports:
      - "9000:9000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
"docker-compose.yaml" с содержимым:
```
version: "3"
services:
  registry:
    image: registry:2
    network_mode: host
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

Решение:

Представлено ниже:

![compose up1](https://github.com/user-attachments/assets/9c94394d-0a9b-493a-9a10-8986644df5a6)

отработал только файл compose.yaml . Причина - потому что это имя файла докер обрабатывает в приоритете - by designe.

Созданный docker.yaml c include

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

![compose up2](https://github.com/user-attachments/assets/b5c87827-ee87-47ee-a476-e0d3264bc633)

![docker ps](https://github.com/user-attachments/assets/91e6eac5-0700-4761-bcaf-5be1ea6fba3d)

![obraz](https://github.com/user-attachments/assets/611c60a4-e08c-422b-b564-34fdb4ea6a14)

![5 zadanie](https://github.com/user-attachments/assets/69190065-6f5d-48f2-833b-34f84fd5edb2)

![5-1 zadanie](https://github.com/user-attachments/assets/fa36a91a-3cd1-4357-995b-966210a1121f)

![inspect](https://github.com/user-attachments/assets/73fec467-aadd-4462-b468-a95264f36f91)

![udalenie](https://github.com/user-attachments/assets/218caac9-c69f-4da4-8ae4-a806af56a998)

- WARN[0000] /root/task5/docker-compose.yaml: version is obsolete - означает предупреждение, что версия устарела (видимо самого файла, т.к. содержимое файла не соотвествует запущенным сервисам).

- WARN[0000] Found orphan containers ([task5-portainer-1]) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.- означает предупреждение, что найдены контейнеры, которые не описаны в файле. для очистки их выполнить с флагом --remove-orphans :

![docker remove](https://github.com/user-attachments/assets/842e2354-b301-4f5e-a2f9-8bf27807edbf)

![docker ps](https://github.com/user-attachments/assets/748bf0e3-3ef9-4c69-8cc8-d4833f79ca48)

![docker down](https://github.com/user-attachments/assets/fac1642f-ae0e-4978-951f-603a54408e3e)

---

### Правила приема

Домашнее задание выполните в файле readme.md в GitHub-репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.


