# FOODGRAM

FOODGRAM это удобный сайт для размещения и поиска рецептов.

### Технологии:

Python, Django, Docker, Gunicorn, NGINX, PostgreSQL, Yandex Cloud.

### Для запуска проекта необходимо:

- Клонировать репозиторий:
```
https://github.com/itsqntz/foodgram-project-react.git
```
- На удаленном сервере необходимо произвести установку необходимых пакетов для docker и docker-compose:

```
sudo apt install docker.io 
```
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
- Локально отредактируйте файл infra/nginx.conf и в строке server_name впишите свой IP.
- Скопируйте файлы docker-compose.yml и nginx.conf из директории infra на сервер:
```
scp docker-compose.yml <username>@<host>:/home/<username>/docker-compose.yml
scp nginx.conf <username>@<host>:/home/<username>/nginx.conf
```
- Cоздайте .env файл и впишите:
```
DB_ENGINE=<django.db.backends.postgresql>
POSTGRES_NAME=<имя базы данных postgres>
POSTGRES_NAME_USER=<пользователь бд>
POSTGRES_NAME_PASSWORD=<пароль>
DB_HOST=<db>
DB_PORT=<5432>
SECRET_KEY=<секретный ключ проекта django>
```
- Теперь проект можно запустить на сервере:
```
sudo docker-compose up -d --build 
```
### Настройка бекенда:
Для корректной работы бекенда необходимо выполнить следующие операции:
- Выполнить миграции для приложений users и recipes:
```
sudo docker-compose exec backend python manage.py migrate
```
- Собрать необходимые статические файлы:
```
sudo docker-compose exec backend python manage.py collectstatic --no-input
```
- Добавить данные об ингредиентах и тегах из заранее заготовленных файлов (по желанию):
```
sudo docker-compose exec backend python manage.py load_data
```
- Создать суперпользователя Django:
```
sudo docker-compose exec backend python manage.py createsuperuser
```
Проект будет доступен по открытому IP вашего сервера.

### Готовый проект можно посмотреть по [адресу](http://51.250.109.198/recipes).

- Данные админки:
```
Логин: admin
Email: admin@ya.ru
Пароль: Admin0709
```

[![Python](https://img.shields.io/badge/-Python-464646?style=flat-square&logo=Python)](https://www.python.org/) [![Django](https://img.shields.io/badge/-Django-464646?style=flat-square&logo=Django)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat-square&logo=Django%20REST%20Framework)](https://www.django-rest-framework.org/)
[![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-464646?style=flat-square&logo=PostgreSQL)](https://www.postgresql.org/)
[![Nginx](https://img.shields.io/badge/-NGINX-464646?style=flat-square&logo=NGINX)](https://nginx.org/ru/)
[![gunicorn](https://img.shields.io/badge/-gunicorn-464646?style=flat-square&logo=gunicorn)](https://gunicorn.org/)
[![docker](https://img.shields.io/badge/-Docker-464646?style=flat-square&logo=docker)](https://www.docker.com/)
[![GitHub%20Actions](https://img.shields.io/badge/-GitHub%20Actions-464646?style=flat-square&logo=GitHub%20actions)](https://github.com/features/actions)
[![Yandex.Cloud](https://img.shields.io/badge/-Yandex.Cloud-464646?style=flat-square&logo=Yandex.Cloud)](https://cloud.yandex.ru/)
![example workflow](https://github.com/itsqntz/foodgram-project-react/actions/workflows/foodgram_workflow.yml/badge.svg)
