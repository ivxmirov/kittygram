[![GitHub%20Actions](https://img.shields.io/badge/-GitHub%20Actions-464646?style=flat-square&logo=GitHub%20actions)](https://github.com/features/actions)
[![docker](https://img.shields.io/badge/-Docker-464646?style=flat-square&logo=docker)](https://www.docker.com)
[![Python](https://img.shields.io/badge/-Python-464646?style=flat-square&logo=Python)](https://www.python.org)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat-square&logo=Django)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat-square&logo=Django%20REST%20Framework)](https://www.django-rest-framework.org)
[![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-464646?style=flat-square&logo=PostgreSQL)](https://www.postgresql.org)
[![gunicorn](https://img.shields.io/badge/-gunicorn-464646?style=flat-square&logo=gunicorn)](https://gunicorn.org)
[![Nginx](https://img.shields.io/badge/-NGINX-464646?style=flat-square&logo=NGINX)](https://nginx.org/ru)

# Kittygram - соцсеть для кошек. Версия Docker + CD/CI GitHub Actions.

**Это социальная сеть для обмена фотографиями любимых питомцев - это полная рабочая платформа, разработанная с использованием Django в качестве бэкенд-фреймворка и React в качестве фронтенд-библиотеки. Деплой на сервер реализован с помощью контейнизатора приложений Docker и технологии автоматизации тестирования и доставки новых модулей проекта - CD/CI**

Бэкенд-приложение на Django предоставляет RESTful API для взаимодействия с базой данных, обработки запросов от клиентов и выполнения бизнес-логики. Здесь реализованы модели данных для пользователей, питомцев, фотографий и других связанных сущностей. Также бэкенд предоставляет эндпоинты для регистрации и аутентификации пользователей, добавления новых питомцев и загрузки фотографий. Фронтенд-приложение на React взаимодействует с бэкендом через API, получая данные и отправляя запросы на создание, обновление и удаление объектов. На фронтенде реализованы страницы для просмотра, добавления и редактирования фотографий и профилей питомцев.

Вся система обеспечивает безопасность данных пользователей, используя механизм аутентификации и авторизации Django. Она также поддерживает масштабирование благодаря использованию Django ORM для работы с базой данных и React-компонентной архитектуры для удобного добавления новых функций и страниц.

Деплой на сервер реализован с помощью технологии CD/CI - автоматического тестирования корректности интеграции обновленного кода запускаямого с помощью GitHub Actions. Сразу после push-а в ветку main реализовано тестирование и заливка контейнеров на DockerHub, обновление кода на рабочем сервере и перезапуск проекта.

Этот проект может быть запущен на сервере или на локальной машине после установки всех зависимостей. В дополнение к тому, это открытый исходный код, поэтому вы можете адаптировать его под свои потребности или вносить свои изменения.

Данный проект тестово запущен и доступен по адресу https://ivxforstudy.ru/, вы можете зайти и ознакомиться с функционалом. \

# Технологии 
### 1. Frontend:
- Node.js
- React

\* Полный список библиотек в файле packeje.json

### 2. Backend:
- Django
- DRF
- Gunicorn
- Pillow

\* Полный список библиотек в файле requirements.txt

### 3. Сервер:
- nginx

### 4. DevOps:
- Docker
- CD/CI GitActions

# Развертывание 

1. Откройте терминал и перейдите в скрытую директорию .ssh — из любой директории выполните команду:

```
cd ~/.ssh
```

2. В директории .ssh создайте новую директорию для SSH-ключей. Выполните команду:
```
mkdir название-директории
```

3. Перенесите файл SSH-ключa в только что созданную директорию

4. Установите права доступа к файлам SSH-ключей с помощью команд:
```
chmod 600 название_файла_закрытого_SSH-ключа
```
5. Введите команду:
```
ssh -i путь_до_файла_с_SSH_ключом/название_файла_с_SSH_ключом login@ip
```
6. Обновлиту список доступных пакетов (здесь и далее развертка для linux-подобных систем, если у вас Windows - используйте команды без 'sudo'):
```
sudo apt update
```
7. проверьте установлен ли Git:
```
git --version
```

если нет то установите: 
```
sudo apt install git
```
для Windows перейдите по [ссылке](https://gitforwindows.org/) и следуйте инструкциям.

8. Сгенерируйте SSH ключ и добавьте на GitHub:
```
ssh-keygen
```
9. Сделайте Fork и клонируйте репозиторий: 
```
git clone git@github.com:Ваш_аккаунт/kittygram_final.git
```
10. Далее установите на сервер пакетный менеджер и утилиту для создания виртуального окружения. Сделать это можно одной командой, перечислив все необходимые к установке пакеты:
```
sudo apt install python3-pip python3-venv -y
```
11. Далее начинайте работать с зависимостями. Перейдите в директорию с бэкенд-приложением проекта, создайте и активируйте виртуальное окружение, установите пакеты из файла requirements.txt:
```
# Переходим в директорию backend-приложения проекта.
cd /backend/

# Создаём виртуальное окружение.
python3 -m venv venv

# Активируем виртуальное окружение.
source venv/bin/activate

# Возвращаемся назад 
cd ..

# Устанавливаем зависимости.
pip install -r requirements.txt
```

12. В корне проекта создайте файл .env с переменными: \
SECRET_KEY= прим. секретный код Джанго приложения. \
ALLOWED_HOSTS= без кавычек, через пробел. \
DB_HOST= \
DB_PORT= \
POSTGRES_DB= \
POSTGRES_USER= \
POSTGRES_PASSWORD= \
DB_NAME= 

13. В настройках репозитория github создайте секретные переменные необходимые для запуска workflow (см. файл /.git/workflows/main.py),
а также все переменные из файла .env из пункта выше. \
TELEGRAM_TO - ваш id аккаунта в телеграмм. \
TELEGRAM_TOKEN - токен бота (можно зарегистрировать у botfather), не забудьте начать с ним диалог, так как бот не может первым начать беседу. \
SSH_PASSPHRASE - пароль к рабочему серверу (продакшн). \
USER - ваш логин учетки рабочего сервера. \
SSH_KEY - закрытый ключ. \
HOST это IP рабочего сервера. \
DOCKER_USERNAME - логин вашего dockerhub. \
DOCKER_PASSWORD - пароль вашего dockerhub.

14. Сбилдите образа и залейте их на dockerhub, обратите внимание, образ kittygram_gateway собирается на основании папки nginx/.
Вместо username подставьте свой username на dockerhub.
```
cd frontend
docker build -t username/kittygram_frontend .
cd ../backend
docker build -t username/kittygram_backend .
cd ../nginx
docker build -t username/kittygram_gateway .

docker push username/kittygram_frontend
docker push username/kittygram_backend
docker push username/kittygram_gateway
```

15. Замените в файле /.git/workflows/main.py логины в переменных с адресами образов на dockerhub-е на свой никнейм.

16. Подготовьте удаленный сервер:
 Через редактор Nano откройте файл конфигурации веб-сервера:
```
sudo nano /etc/nginx/sites-enabled/default
```
 Удалите все настройки из файла, запишите и сохраните новые:
```
server {
    server_tokens off;
    server_name ваше доменное имя;

    location / {
        proxy_pass http://127.0.0.1:9000;
    }
}
```

17. Устновите ssl-сертификаты: 
[Ссылка на certbot](https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal) 


18. Сохраните изменения, проверьте и перезагрузите конфигурацию веб-сервера:
```
sudo nginx -t
sudo systemctl reload nginx
```

19. В корне рабочей директории создайте папку с проектом и перейдите в нее:
```
mkdir kittygram
cd kittygram
```

20. Копируйте в директорию файл docker-compose.production.yml и .env и запустите Docker Compose в режиме демона:
```
sudo docker compose -f docker-compose.production.yml up -d
```

Теперь на сервере крутится целый флот контейнеров, объединённых в сеть. Docker Compose работает в фоне, но в любой момент готов принять ваши команды. Выполнять команды docker compose нужно из той директории, в которой размещён файл конфигурации.
Основные команды, которые вам понадобятся для управления:

- docker compose stop — остановит все контейнеры, но оставит сети и volume. Эта команда пригодится, чтобы перезагрузить или обновить приложения.
- docker compose down — остановит все контейнеры, удалит их, сети и анонимные volumes. Можно будет начать всё заново.
- docker compose logs — просмотр логов запущенных контейнеров.

21. Проверьте, что все нужные контейнеры запущены:
```
sudo docker compose -f docker-compose.production.yml ps
```

22. Выполните миграции, соберите статические файлы бэкенда и скопируйте их в /backend_static/static/:
```
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /backend_static/static/
```

**Все, теперь сайт запущен и доступен по адресу вашего доменного имени, которое вы вписали в файл конфигурации nginx.**

**Новые обновления кода, запушеные в ветку main, будут автоматически проверяться и сразу же деплоиться на рабочий сервер.**
 

### Автор 
- Хмыров Илья - [GitHub](https://github.com/ivxmirov)
