# recsys_workshop

Набор данных для демонстрации работы рекомендательной системы

# Содержание

Датасет содержит файлы
* ноутбук `recsys_demo_workshop.ipynb`
* csv `data/user_item_views.zip` на ~2 млн строк вида

| user_id | item_id	| show_timestamp | show_duration |
| --- | --- | --- | --- |
| 912948920 | 1587935070 | 1119307 | 323 |

* архив `data/content_catalog.zip` содержит csv формата

| item_id | title |
| --- | --- |
| 1593139110 | Тачки 3 |

* архив `data/json_views.tar.gz` содержит single-line JSON вида

```json
{"value": 6127, "date": 1606254752, "validation": 0, "item_id": 930420160, "user_id": 399644822}
```

* pickle `data/ground_truth_dataset.pkl` с просмотрами контента за 1 день по 13353 пользователям
* pickle `data/test_dataset.pkl` с просмотрами контента за 180 предшествующих дней по 13353 пользователям

Бинарный файл `ground_truth_dataset.pkl` (`test_dataset.pkl`) это массив где каждый элемент представляет собой
записи из `data/json_views.tar.gz` агрегированные по полю `user_id` в словарь вида `{item_id: value, ..., iеem_id: value}`,
с флагом `is_validation=1` (`is_validation=0`).

# Эксплуатация

В директории с ноутбуком запустить код

```shell
docker run --rm -p 10000:8888 -e JUPYTER_ENABLE_LAB=yes -v "$PWD":/home/jovyan/work jupyter/datascience-notebook:python-3.8.6
```

Если будем использовать mongo, redis - нужно подключить контейнер в общую сеть

```shell
docker run --rm --network data-mng_aviation_network -p 10000:8888 -e JUPYTER_ENABLE_LAB=yes -v "$PWD":/home/jovyan/work jupyter/datascience-notebook:python-3.8.6
```
