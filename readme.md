# Домашнее задание модуля

## Текст задания

Сейчас наша библиотека отражает, какие книги у нас есть. Что, если ваш друг попросит у вас что-то почитать? Для того чтобы не запутаться и всегда помнить, кому и какую книгу вы отдали, давайте модифицируем наш проект.

Нам нужно добавить модель "Друга" и описать для неё необходимые поля. [x] Знания о полях можно освежить в (документации) [https://docs.djangoproject.com/en/2.2/ref/models/fields/].

Кроме этого, вероятно, потребуется внести изменения в уже существующие модели, чтобы отразить отношения моделей "Книга" и "Друг". Мы должны понимать, какие книги были одолжены, кому они были одолжены. [x]

Добавьте несколько записей в таблицу друзей для того, чтобы можно было легко проверить работу приложения. [x]

## Создаем виртуальное окружение

`$ python3 -m venv D5_HW_env` - cоздаем виртуальное окружение для проекта, находящегося в соответствующей папке, где D5_HW_env - название виртуального окружения.
`$ source D5_HW_env/bin/activate` - активируем виртуальное окружение . где `$ source D5_HW_env/bin/activate` — это имя виртуального окружения.
`pip3 install -r my_requirements.txt` - устанавливаем зависимости
Настроили файл settings.py для работы локального сервера:
SECRET_KEY
ALLOWED_HOSTS
DATABASES
STATIC_URL
STATIC_ROOT - закомментировать

В виртуальной среде Python 3 вместо команды python3 можно использовать python, а вместо pip3 — pip.

## Выполнение домашнего задания

Создаем модель Друг

```python
class Friend(models.Model):
  full_name = models.TextField()
  birth_year = models.SmallIntegerField()
  address = models.TextField()
  e_mail = models.EmailField()

  def __str__(self):
    return self.full_name
```

Вносим изменения в модель Книга для связи с моделью Друг
`friend = models.ForeignKey("p_library.Friend", on_delete=models.SET_NULL, verbose_name=_("Читатель"), related_name="book_reader", null=True)`
`python manage.py makemigrations` - создали файл миграции
`python manage.py migrate` - применили миграции

Добавил в admin.py новую панель

```python
from p_library.models import Book, Author, Publisher, Friend

@admin.register(Friend)
class FriendAdmin(admin.ModelAdmin):
    pass
```

В admin.py разрешил показ поля `friend` в панели Book: `fields = ('ISBN', 'title', 'description', 'year_release', 'author', 'price', 'publisher', 'friend')`
С помощью админки добавил четырех друзей.

## Полезные команды

`$ python3 -m venv D2_env` - cоздаем виртуальное окружение для проекта, находящегося в соответствующей папке, где D2_env - название виртуального окружения.

`$ source D2_env/bin/activate` - активируем виртуальное окружение, где D2_env — имя виртуального окружения.

`$ deactivate` - деактивация виртуального окружения

`$ pip3 freeze > requirements.txt` - сохраняем зависимости

`$ pip3 install -r requirements.txt` - устанавливаем зависимости

`$ python manage.py runserver` - запускаем сервер Джанго

## Порядок проверки домашнего задания

1. Скачиваем проект
2. Создаем виртуальное окружение
3. Устанавливаем зависимости
4. Запускаем сервер Джанго
5. Проверяем ДЗ. С вопросами обращаться в личку в слаке. Я там под своим именем - Павел Гвоздев.
6. Хорошего дня!
