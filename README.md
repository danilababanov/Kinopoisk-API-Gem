# КиноПоиск API (Gem)

Гем основан на API от Andrzej Wielski: http://docs.kinopoiskapi.apiary.io/. Спасибо автору за такую великолепную реализацию.

Этот gem создан для упрощения работы с КиноПоиск API в проектах Ruby on Rails.

## Установка

Добавьте эту строку в Gemfile вашего приложения:

```ruby
gem 'KinopoiskAPI' , github: 'afuno/Kinopoisk-API-Gem', branch: 'master'
```

Затем выполните:

    $ bundle


## Использование

### Фильм

```ruby
film = KinopoiskAPI::Film.new(733493)
```
```ruby
#   Вся информация о фильме
film.all
```
```ruby
#   Название фильма на русском
film.title[:ru]
```
```ruby
#   Название фильма на английском
film.title[:en]
```

Доступен вывод следующей информации:

* **id** - КиноПоиск ID
* **url** - URL адрес страницы на КиноПоиск
* **title** - Названия:
    * **ru** - На русском
    * **en** - На английском
* **slogan** - Слоган
* **description** - Описание
* **poster** - Полный адрес на постер (в формате JPG)
* **year** - Год выхода
* **kinopoisk** - Массив следующих данных для КиноПоиск:
    * **rating** - Рейтинг
    * **quantity** - Количество оценивших
    * **good_reviews_in_percentage** - Количество положительных рецензий в процентах
    * **number_of_good_reviews** - Количество положительных рецензий
    * **waiting_in_percentage** - Количество ожидающих в процентах
    * **number_of_waiting** - Количество ожидающих
    * **film_critics_in_percentage** - Положительны рейтинг критиков в мире в процентах
    * **film_critics** - Количество положительных оценок критиков в мире
    * **rf_critics_in_percentage** - Положительны рейтинг критиков в РФ в процентах
    * **rf_critics** - Количество положительных оценок критиков в РФ
* **imdb** - Массив следующих данных для IMDb:
    * **id** - IMDb ID
    * **rating** - Рейтинг
    * **quantity** - Количество оценивших
* **number_of_reviews** - Количество рецензий
* **duration** - Продолжительность фильма
* **countries** - Массив со странами
* **genres** - Массив с жанрами
* **video** - Полный адрес на трейлер
* **is_sequel_or_prequel** - Имеет ли сиквелы или приквелы
* **is_similar_films** - Имеет ли родственные фильмы
* **is_imax** - Есть ли IMAX
* **is_3d** - Есть ли 3D
* **rating_mpaa** - Рейтинг MPAA
* **minimal_age** - Минимальный рекомендуемый возраст
* **premiere** - Массив данных о премьере:
    * **ru** - Дата премьеры в РФ
    * **world** - Дата премьеры в мире
    * **world_country** - Страна премьеры
* **status** - Проверка полученного JSON (true или false)

### Режисеры, актеры, операторы и т. д.

```ruby
staff = KinopoiskAPI::Staff.new(733493)
```
```ruby
#   Все имена всех профессий
staff.all
```
```ruby
#   Все имена одной профессии
staff.profession('writer')
```

Доступен вывод следующей информации:

* **id** - Идентификатор имени на сайте КиноПоиск
* **url** - URL на страницу именина КиноПоиск
* **full_name** - Имена:
    * **ru** - На русском
    * **en** - На английском
* **poster** - Полный адрес на постер (в формате JPG)
* **profession** - Профессия на русском (актер, режиссер и т. д.)
* **status** - Проверка полученного JSON (true или false)

### Галерея

```ruby
gallery = KinopoiskAPI::Gallery.new(733493)
```
```ruby
#   Все изображения из всех разделов
gallery.all
```
```ruby
#   Все изображения из конкретного раздела
gallery.section('poster')
```

Доступен вывод следующей информации:

* **image** - Полный адрес на полное изображение (в формате JPG)
* **preview** - Полный адрес на превью (в формате JPG)
* **status** - Проверка полученного JSON (true или false)

### Похожие

```ruby
similar = KinopoiskAPI::Similar.new(733493)
```
```ruby
#   Все похожие фильмы
similar.all
```

Доступен вывод следующей информации:

* **title** - Названия:
    * **ru** - На русском
    * **en** - На английском
* **year** - Год выхода
* **rating** - Рейтинг
* **number_of_rated** - Количество оценивших
* **poster** - Полный адрес на постер (в формате JPG)
* **duration** - Продолжительность фильма
* **countries** - Массив со странами
* **genres** - Массив с жанрами
* **status** - Проверка полученного JSON (true или false)

### Жанры

```ruby
genres = KinopoiskAPI::Genres.new
```
```ruby
#   Все жанры
genres.all
```

Доступен вывод следующей информации:

* **id** - Идентификатор жанра на сайте КиноПоиск
* **name** - Жанр на русском
* **status** - Проверка полученного JSON (true или false)

### Глобавльный поиск

```ruby
global_search = KinopoiskAPI::GlobalSearch.new('Звездные')
```
```ruby
#   Скорее всего вы искали этот фильм
global_search.exactly
```
```ruby
#   Возможно, вы искали эти фильмы
global_search.maybe
```
```ruby
#   Или даже этих людей
global_search.names
```

Доступен вывод следующей информации:

* **all** - Полный массив данных
* **keyword** - Ключевое слово (запрос)
* **number_of_films** - Количество найденных фильмов по ключевому слову
* **number_of_names** - Количество найденных имен по ключевому слову
* **exactly** - Один, наиболее подходящий фильм:
    * **title** - Названия:
        * **ru** - На русском
        * **en** - На английском
    * **info** - Краткая информация
    * **duration** - Продолжительность фильма
    * **year** - Год выхода
    * **countries** - Массив со странами
    * **genres** - Массив с жанрами
    * **rating** - Рейтинг
    * **number_of_rated** - Количество оценивших
    * **poster** - Полный адрес на постер (в формате JPG)
* **maybe** - Список фильмов, которые также подходят под запрос:
    * **title** - Названия:
        * **ru** - На русском
        * **en** - На английском
    * **info** - Краткая информация
    * **duration** - Продолжительность фильма
    * **year** - Год выхода
    * **countries** - Массив со странами
    * **genres** - Массив с жанрами
    * **rating** - Рейтинг
    * **number_of_rated** - Количество оценивших
    * **poster** - Полный адрес на постер (в формате JPG)
* **names** - Список имен, которые также подходят под запрос:
    * **full_name** - Имена:
        * **ru** - На русском
        * **en** - На английском
    * **info** - Краткая информация
    * **poster** - Полный адрес на постер (в формате JPG)
* **status** - Проверка полученного JSON (true или false)

### Рецензии

```ruby
reviews = KinopoiskAPI::Reviews.new(733493)
```
```ruby
#   Количество рецензий
reviews.quantity[:reviews]
```
```ruby
#   Рецензии
reviews.reviews
```

Доступен вывод следующей информации:

* **all** - Полный массив данных
* **pages** - Количество страниц
* **page** - Текущая страница
* **quantity** - Массив следующих данных:
    * **reviews** - Количество рецензий
    * **good_reviews** - Количество положительных рецензий
    * **good_reviews_in_percent** - Количество положительных рецензий в процентах
    * **bad_reviews** - Количество отризательных рецензий
    * **neutral_reviews** - Количество нейтральных рецензий
* **reviews** - Список рецензий:
    * **id** - Идентификатор на КиноПоиск
    * **type** - Тип: положительный, негативный или нейтральный
    * **data** - Дата и время публикации
    * **author** - Массив данных об авторе:
        * **name** - Имя (или никнейм) автора рецензии
        * **avatar** - Полный адрес на аватар (в формате JPG)
    * **title** - Заголовок
    * **description** - Описание
* **status** - Проверка полученного JSON (true или false)

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

