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

[![imageup.ru](https://imageup.ru/img258/3625614/screenshot-from-2020-06-30-17-00-33.png)](https://imageup.ru/img258/3625614/screenshot-from-2020-06-30-17-00-33.png.html)

## 2. Создать любой Flume поток используя Flume сервис соответствующего номера.

- Тип источника источник – exeс
- Тип канала – memory
- Тип слива – hdfs

[![imageup.ru](https://imageup.ru/img110/3625613/screenshot-from-2020-06-30-16-59-50.jpg)](https://imageup.ru/img110/3625613/screenshot-from-2020-06-30-16-59-50.jpg.html)

## 3. Убедиться что данные поступают в слив.
```
[student4_13@node1 ~]$ echo "dada" >> /tmp/data
[student4_13@node1 ~]$ hdfs dfs -ls /flume/Flume4_13
Found 1 items
drwxr-xr-x   - flume flume          0 2020-06-30 13:58 /flume/Flume4_13/20-06-30
```

## 4. Создать поверх данных в hdfs таблицу через которую можно просмотреть полученные данные.


