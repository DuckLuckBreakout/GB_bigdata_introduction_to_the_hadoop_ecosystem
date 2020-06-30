# Для части по SQOOP
## Провести импорт таблицы из вашего сервера БД в Hadoop с использованием SQOOP в любых двух вариантах из перечисленных ниже.

a. в Hive-таблицу (`--hive-import`)

b. в HDFS в формате avro (`--as-avrodatafile`)

c. в HDFS в формате sequencefile (`--as-sequencefile`)

### a. в Hive-таблицу (`--hive-import`)
```
[student4_13@node3 ~]$ sqoop import --connect jdbc:postgresql://node3.novalocal/pg_db --username exporter -P --table character --hive-import --hive-database student4_13 --hive-table character
```
[![imageup.ru](https://imageup.ru/img202/3625526/screenshot-from-2020-06-30-12-07-31.png)](https://imageup.ru/img202/3625526/screenshot-from-2020-06-30-12-07-31.png.html)
### b. в HDFS в формате avro (`--as-avrodatafile`)
```
[student4_13@node3 ~]$ sqoop import --connect jdbc:postgresql://node3.novalocal/pg_db --table sales_large -m 1 --target-dir /student4_13/tables/sales_large --as-avrodatafile --username exporter -P
```
[![imageup.ru](https://imageup.ru/img93/3625536/screenshot-from-2020-06-30-12-41-51.png)](https://imageup.ru/img93/3625536/screenshot-from-2020-06-30-12-41-51.png.html)


# Для части по потоковой обработке (Flume)

## 1. Создать Flume-агент с именем, соответствующим имени своего пользователя (например Flume4_20)

## 2. Создать любой Flume поток используя Flume сервис соответствующего номера.

- Тип источника источник – exeс
- Тип канала – memory
- Тип слива – hdfs

[![imageup.ru](https://imageup.ru/img202/3625606/screenshot-from-2020-06-30-15-53-39.jpg)](https://imageup.ru/img202/3625606/screenshot-from-2020-06-30-15-53-39.jpg.html)

## 3. Убедиться что данные поступают в слив.

## 4. Создать поверх данных в hdfs таблицу через которую можно просмотреть полученные данные.

## 5. [Продвинутый вариант] Сделать то-же самое используя несколько сливов в разные места, например в HDFS и в HIve одновременно

## 6. [Продвинутый вариант] Повторить стандартный пример с выборкой сообщений из Twitter.
