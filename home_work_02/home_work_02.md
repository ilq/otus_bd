1. Проводим анализ возможных запросов\отчетов\поиска данных.
* Список оцененных фильмов
* Список фильмов из wish-list'а
* Список совкусников с коэффициентом совпадения вкусов
* Список фильмов у другого пользователя
* Список фильмов ТОП-X у всех совкусников с коэффициентом больше определенного
* Поиск по названию фильма
* Поиск по жанру

2. Создаем дополнительные индексы - простые или композитные. На каждый индекс пишем краткое описание зачем он нужен (почему по этому полю\полям).
   1. при поиске совкусников может понадобиться индекс для Contaste.percent
      * CREATE INDEX ON Contaste (percent);
   2. При поиске фильма по названию понадобится индекс Film.name
      * CREATE INDEX ON Film (upper(name));

3. Думаем какие логические ограничения в БД нужно добавить - например какие поля должны быть уникальны, в какие нужно добавить условия, чтобы не нарушить бизнес логику. Пример - нельзя провести операцию по переводу средств на отрицательную сумму. Создаем ограничения по выбранным полям.
   1. Уникальным должен быть login у User.username
      * username varchar UNIQUE,
   2. На Foreign Key создаём ограничения, например:
      * CREATE TABLE Film (..., ganre_id integer REFERENCES Ganre ON DELETE RESTRICT);