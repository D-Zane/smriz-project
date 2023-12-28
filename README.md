## Проект по СМРИЗ

Продуктовый помощник с базой кулинарных рецептов. Позволяет публиковать рецепты, сохранять избранные, а также формировать список покупок для выбранных рецептов. Можно подписываться на любимых авторов.


### Технологии:

Python, Django, Django Rest Framework, Docker, Gunicorn, NGINX, PostgreSQL, Yandex Cloud, Continuous Integration, Continuous Deployment

### Запуск проекта:


- В директории infra создать файл .env и заполнить данными:
```
DB_ENGINE=django.db.backends.postgresql
POSTGRES_DB=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
SECRET_KEY='секретный ключ Django'
```

- Создать и запустить контейнеры Docker, последовательно выполнить команды по созданию миграций, сбору статики, 
созданию суперпользователя, как указано выше.
```
docker-compose -f docker-compose.yml up -d
```


- После запуска проект будут доступен по адресу: [http://localhost/](http://localhost/)


- Документация будет доступна по адресу: [http://localhost/api/docs/](http://localhost/api/docs/)

В документации описаны возможные запросы к API и структура ожидаемых ответов. Для каждого запроса указаны уровни прав доступа.

- После успешной сборки выполнить миграции:
```
docker compose exec backend python manage.py migrate
```

- Создать суперпользователя:
```
docker compose exec backend python manage.py createsuperuser
```
- Существующий созданный суперпользователь
```
E-mail - theangryzane@gmail.com
Password - 1
```
- Собрать статику:
```
docker compose exec backend python manage.py collectstatic --noinput
```

- Наполнить базу данных содержимым из файла ingredients.json:
```
docker compose exec backend python manage.py loaddata ingredients.json
```

- Для остановки контейнеров Docker:
```
docker compose down -v      # с их удалением
docker compose stop         # без удаления
```


### Авторы:

Савенков Дмитрий, Дарья Лоткова МПИ-23-1-2
