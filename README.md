# Проект: docker
## Описание

Репозиторий содержить конфигурацию docker-compose (docker-compose.yml)
и конфигурацию веб-сервера nginx (nginx/development/default.conf) для выполнения 
развертывания проекта агрегатор товаров.

## Docker-compose

Docker Compose — это инструментальное средство, входящее в состав Docker. 
Оно предназначено для решения задач, связанных с развёртыванием проектов.
Позволяет запускать множество контейнеров одновременно и маршрутизировать 
потоки данных между ними.

Агрегатор товаров состоит из трех Docker контейнеров:
 - dev_db - postgres БД
 - dev_backend - django REST framework приложение
 - dev_web - nginx + ReactJS

Настройки контейнеров расположены в репозиториях 
web-project-backend и web-project-frontend:
 - web-project-backend/Dockerfile
 - web-project-frontend/Dockerfile

### Команды для запуска и настройки контейнеров:

Сборка из образов и поднятие Docker контейнеров:
```
docker-compose up -d --build
```

Выполение команд внутри контейнера dev_backend:
```
docker-compose exec web python manage.py makemigrations
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
```

Просмотр логов запущенных приложений в соответствующих контейнерах:

```
docker logs --tail 50 --follow --timestamps dev_db
docker logs --tail 50 --follow --timestamps dev_backend
docker logs --tail 50 --follow --timestamps dev_web
```


## Nginx

Nginx - веб-сервер и прокси-сервер, работающий на Unix-подобных операционных системах.
В данном проекте nginx выполняет перенаправление (проксирование) запросов клиента на 
сторону backend сервиса и отвечает за раздачу статических файлов.
