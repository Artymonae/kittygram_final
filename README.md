[![Main Kittygram workflow](https://github.com/artymonae/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/artymonae/kittygram_final/actions/workflows/main.yml)
# Проект: Kittygram
### Учебный проект *Яндекс.Практикум* курса Python-разработчик(backend)


Проект Kittygram предназначен для публикации фото котиков и только котиков, никаких собак.
Чем милее котик - тем больше вы получите social credit!

[](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExYjN1OWcxNWd2YTJ3cmRob3JieTNndHBsaDI2ZDNoNnBzeGR4YWMzcyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/EvN5Pe56MOPJY7JmHR/giphy.gif)

## Технологии
[Python](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExZG8wOGVqNDV3ZTA2Z2pnYTFrY2hndms3ZHc2OW05MmIybDJqMHdvbiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/KAq5w47R9rmTuvWOWa/giphy.gif)
![Django](https://img.shields.io/badge/Django-092E20?logo=django&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?logo=postgresql&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?logo=react&logoColor=black)
![Nginx](https://img.shields.io/badge/Nginx-009639?logo=nginx&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=github-actions&logoColor=white)



## Запуск проекта на удаленном сервере.

1. Установить docker compose на сервер:
```bash
sudo apt update
```
```bash
sudo apt install curl
```
```bash
curl -fSL https://get.docker.com -o get-docker.sh
```
```bash
sudo sh ./get-docker.sh
```
```bash
sudo apt-get install docker-compose-plugin
```

2. Скачать файл [docker-compose.production.yml](https://github.com/artymonae/kittygram_final/blob/main/docker-compose.production.yml) на свой сервер.

3. На сервере в директории с файлом **docker-compose.production.yml** создать файл  **.env**:
``` bash
POSTGRES_DB=имя базы данных
POSTGRES_USER=владелец базы данных
POSTGRES_PASSWORD=пароль базы данных
DB_HOST=db
DB_PORT=5432
SECRET_KEY=ключ приложения django
DEBUG=True/False
ALLOWED_HOSTS=разрешенные хосты(your.domain.com)
```
4. Запустить Docker compose:
``` bash
sudo docker compose -f docker-compose.production.yml up -d
```
5. На сервере настроить и запустить Nginx:
- Открыть файлы конфигурации
    ``` bash
    sudo nano /etc/nginx/sites-enabled/default
    ```
- Внести изменения, заменив **<your.domain.com>** на свое доменное имя
    ``` bash 
    server {
        listen 80;
        server_name <your.domain.com>;

        location / {
            proxy_set_header Host $http_host;
            proxy_pass http://127.0.0.1:9000;
            client_max_body_size 20M;
        }
    }
    ```
- Убедиться, что в файле конфигурации нет ошибок
    ``` bash
    sudo nginx -t
    ```
- Перезагрузить конфигурацию
    ``` bash
    sudo service nginx reload
    ```

## Автор проекта [**Артем Болдырев**](https://github.com/artymonae)