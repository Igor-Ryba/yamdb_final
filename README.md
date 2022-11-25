![Cтатус workflow](https://github.com/Igor-Ryba/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

# Проект YamDB
## **Описание**

Сайт с отзывами о произведениях культуры различных направлений.

Ссылка на развернутый проект:
http://51.250.29.87/redoc/

## **Как запустить проект:**

В директории infra/ создаем файл .env со следующим наполнением:
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres 
POSTGRES_USER=user
POSTGRES_PASSWORD= password
DB_HOST=db
DB_PORT=5432


Клонируем репозиторий:
git clone git@github.com:Igor-Ryba/yamdb_final.git

Запускаем docker-compose.yaml
docker-compose up

Пересобираем контейнер:
docker-compose up -d --build

docker-compose exec web python manage.py migrate

Создаем суперпользователя (вводим почту, логин, пароль):
docker-compose exec web python manage.py createsuperuser

Собираем статику:
docker-compose exec web python manage.py collectstatic --no-input

Наполняем базу из файла с фикстурами:
docker-compose exec web python manage.py dumpdata > fixtures.json

При успешном выполнении предыдущих шагов проект станет доступен по адресу:
http://localhost/admin/

## **Примеры запросов:**

Регистрация нового пользователя http://127.0.0.1/api/v1/auth/signup/
```
POST
/auth/signup/

Request samples:
{
"email": "string",
"username": "string"
}

Response samples:
{
"email": "string",
"username": "string"
}
```
Получение/создание/удаление категорий http://127.0.0.1/api/v1/categories/
```
POST
/categories/

Request samples:
{
"name": "string",
"slug": "string"
}

Response samples:
{
"name": "string",
"slug": "string"
}
```
Получение/создание/удаление жанров http://127.0.0.1/api/v1/genres/
```
GET
/genres/

Response samples:
[
{
"count": 0,
"next": "string",
"previous": "string",
"results": []
}
]

POST
/genres/

Response samples

{
"name": "string",
"slug": "string"
}
```
Получение/создание/удаление/частичное обновление произведений http://127.0.0.1/api/v1/titles/
```
GET
/titles/

Response samples:
[
{
"count": 0,
"next": "string",
"previous": "string",
"results": []
}
]

POST
/titles/

Request samples:
{
"name": "string",
"year": 0,
"description": "string",
"genre": [
"string"
],
"category": "string"
}

Response samples:
{
"id": 0,
"name": "string",
"year": 0,
"rating": 0,
"description": "string",
"genre": [
{}
],
"category": {
"name": "string",
"slug": "string"
}
}

PATCH
/titles/{titles_id}/

Request samples:
{
"name": "string",
"year": 0,
"description": "string",
"genre": [
"string"
],
"category": "string"
}

Response samples:
{
"id": 0,
"name": "string",
"year": 0,
"rating": 0,
"description": "string",
"genre": [
{}
],
"category": {
"name": "string",
"slug": "string"
}
}
