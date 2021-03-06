# Описание задачи

Небольшой интернет-магазин попросил вас добавить ранжирование товаров в блок "смотрели ранее" - в нем теперь надо показывать не последние просмотренные пользователем товары, а те товары из просмотренных, которые он наиболее вероятно купит. Качество вашего решения будет оцениваться по количеству покупок в сравнении с прошлым решением в ходе А/В теста, т.к. по доходу от продаж статзначимость будет достигаться дольше из-за разброса цен. Таким образом, ничего заранее не зная про корелляцию оффлайновых и онлайновых метрик качества, в начале проекта вы можете лишь постараться оптимизировать recall@k и precision@k. Это задание посвящено построению простых бейзлайнов для этой задачи: ранжирование просмотренных товаров по частоте просмотров и по частоте покупок. Эти бейзлайны с одной стороны могут помочь вам грубо оценить возможный эффект от ранжирования товаров в блоке - например, чтобы вписать какие-то числа в коммерческое предложение заказчику, а с другой стороны, могут оказаться самым хорошим вариантом, если данных очень мало (недостаточно для обучения даже простых моделей).

# Входные данные
https://drive.google.com/file/d/0B_XgWOQXdn6jZ2VnNUVWVzhvdm8/view?usp=sharing
https://drive.google.com/file/d/0B_XgWOQXdn6jcy1BOW1weFJNZnM/view?usp=sharing

А также в папке Git-а.

Вам дается две выборки с пользовательскими сессиями - id-шниками просмотренных и id-шниками купленных товаров. Одна выборка будет использоваться для обучения (оценки популярностей товаров), а другая - для теста. 

В файлах записаны сессии по одной в каждой строке. Формат сессии: id просмотренных товаров через "," затем идёт ";" после чего следуют id купленных товаров (если такие имеются), разделённые запятой. Например, "1,2,3,4;" или "1,2,3,4;5,6". Гарантируется, что среди id купленных товаров все различные. 

# Задание

1. На обучении постройте частоты появления id в просмотренных и в купленных (id может несколько раз появляться в просмотренных, все появления надо учитывать) 
2. Реализуйте два алгоритма рекомендаций: сортировка просмотренных id по популярности (частота появления в просмотренных), сортировка просмотренных id по покупаемости (частота появления в покупках). Если частота одинаковая, то сортировать надо по возрастанию момента просмотра (чем раньше появился в просмотренных, тем больше приоритет)
3. Для данных алгоритмов найдите AverageRecall@1, AveragePrecision@1, AverageRecall@5, AveragePrecision@5 на обучающей и тестовых выборках, округляя до 2 знака после запятой. Это будут ваши ответы в этом задании. Отправить нужно через форму https://goo.gl/forms/EBKXxY8w9Oamltyu2

# Дополнительные замечания

1. Когда усредняем precision@k или recall@k по сессиям надо усреднять только для тех сессий, в которых были покупки.
2. Статистика просмотров и покупок строится только по обучающей выборке, а не по сессии к которой делается рекомендация.


# Условие своими словами

Есть обучающая выборка, по ней мы стоим два словаря частот: частоты появлений в просмотренных, частоты появления в покупках. Это в каком-то смысле обучение рекомендательной системы (РС).

Далее нужно сделать применение РС к выборкам (обучающей и тестовой). РС работает так: просмотренные объекты в сессии сортируются по убыванию частоты из словаря РС. Это и есть рекомендация.



