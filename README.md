### taski-docker

## Описание

Через Taski пользователи могут создавать новые задачи и отмечать уже выполненые.

## Как запустить проект на сервере:

Создайте на своем сервере в директорию taski/  и скопируйте файл docker-compose.production.yml. Сделать это можно, например, при помощи утилиты SCP:
```
scp -i path_to_SSH/SSH_name docker-compose.production.yml \
    username@server_ip:/home/username/taski/docker-compose.production.yml
```
Выполните эту команду на сервере в папке taski/:
```
sudo docker compose -f docker-compose.production.yml up -d
```
Выполните миграции, соберите статические файлы бэкенда и скопируйте их в /backend_static/static/:
```
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /static/static/
```
Обновите конфиг Nginx и переагрузите его.
Откройте в браузере страницу проекта https://bountytaski.serveftp.com/
