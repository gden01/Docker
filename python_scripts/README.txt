# Проект PostgreSQL Docker

Этот проект предоставляет инструкции и файлы для создания Docker-контейнера с PostgreSQL и Python-скриптом для работы с базой данных. 

## Как использовать

### Шаг 1: Скачать образ PostgreSQL

Чтобы начать, сначала необходимо скачать официальный образ PostgreSQL с помощью Docker:

```shell
docker pull postgres

Шаг 2: Создать Docker-контейнер

    Пишем инструкции для Dockerfile, используя следующий файл:
# Используем официальный образ PostgreSQL
FROM postgres:latest
ENV POSTGRES_DB=database
ENV POSTGRES_USER=postgres
ENV POSTGRES_PASSWORD=password

# Копируем SQL-скрипт из абсолютного пути в контейнер
COPY init.sql /docker-entrypoint-initdb.d/init.sql
# Этот контейнер использует механизм хранения данных "volume"
# чтобы сохранить данные между перезапусками контейнера
VOLUME data:/var/lib/postgresql/data

# Добавляем команду для запуска Python-скрипта app.py
CMD ["python", "app.py"]

Соберите Docker-контейнер:
docker build -t my-postgres .

Шаг 3: Запустить Docker-контейнер

Вы можете запустить Docker-контейнер с помощью следующей команды, установив пароль для пользователя PostgreSQL:
docker run --name my-postgres-container -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword -d my-postgres

Шаг 4: Проверить работу контейнера

Чтобы убедиться, что контейнер успешно запущен, выполните:
docker ps

Шаг 5: Работа с Python-скриптом

Python-скрипт app.py включает в себя функции для работы с базой данных PostgreSQL. Он подключается к базе данных, извлекает данные и вычисляет индекс массы для пользователей. Вы можете изменить этот скрипт по своему усмотрению.
Структура проекта

    Dockerfile: Файл для создания Docker-контейнера PostgreSQL с Python-скриптом.
    init.sql: SQL-скрипт для инициализации базы данных.
    app.py: Python-скрипт для работы с базой данных PostgreSQL.

Зависимости

    Docker: https://www.docker.com/get-started
    psycopg2: Библиотека Python для работы с PostgreSQL.


