## Описание
Проект YaMDb собирает отзывы пользователей на произведения. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).
Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»).
Добавлять произведения, категории и жанры может только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.
Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.

## Шаблон наполнения .env
.env следует хранить по пути **../infra_sp2/infra/.env**
~~~
DB_ENGINE= указываем название базы данных
DB_NAME= имя базы данных
POSTGRES_USER= логин для подключения к базе данных
POSTGRES_PASSWORD= пароль для подключения к БД
DB_HOST= название сервиса (контейнера)
DB_PORT= порт для подключения к БД
~~~

## Начало работы 
**Запустить проект**

    ../infra-sp2/infra/docker-compose up
**Создать суперпользователя**

    ../docker-compose exec web python manage.py createsuperuser     
## Другие комманды docker 
**Остановить проект**

    ../infra-sp2/infra/docker-compose down
**Октрыть логи сервиса**

    ../infra-sp2/infra/docker-compose logs -f [название сервиса]
   **Вывести список контейнеров**
   
    ../infra-sp2/infra/docker-compose ps
   
   ## Заполнение базы данных
   Данные для тестовой базы данных должны быть расположены в каталоге
```
static/data/
```
### Источники и формат наполнения

	- users.csv [id,username,email,role,bio,first_name,last_name]
	- genre.csv [id,name,slug]
	- category.csv [id,name,slug]
	- titles.csv [id,name,year,category]
	- genre_title.csv [id,title_id,genre_id]
	- review.csv [id,title_id,text,author,score,pub_date]
	- comments.csv [id,review_id,text,author,pub_date]

Для импорта каждого источника подготовалена менеджмент команда:
```python
../docker-compose exec web python manage.py import_from_csv_{имя источника}
```
**Выполнять для импорта тествоой бд**

    ../docker-compose exec web python manage.py import_from_csv_users

    ../docker-compose exec web python manage.py import_from_csv_genre
    
    ../docker-compose exec web python manage.py import_from_csv_category
    
    ../docker-compose exec web python manage.py import_from_csv_titles
    
    ../docker-compose exec web python manage.py import_from_csv_genre_title
    
    ../docker-compose exec web python manage.py import_from_csv_review
    
    ../docker-compose exec web python manage.py import_from_csv_comments
    

Комманды следует выполнять в порядке, перечисленом выше
