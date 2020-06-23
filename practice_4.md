## 1. Создать таблицы в форматах PARQUET/ORC/AVRO c компрессией и без оной. (Выберите один вариант, например ORC с компрессией)

Был выбран формат ORC без компрессии:
[![imageup.ru](https://imageup.ru/img238/3622963/screenshot-from-2020-06-22-17-49-27.png)](https://imageup.ru/img238/3622963/screenshot-from-2020-06-22-17-49-27.png.html)
```sql
CREATE TABLE `student4_13.citation_data_orc`(
	  `oci` string, 
	  `citing` string, 
	  `cited` string, 
	  `creation` string, 
	  `timespan` string, 
	  `journal_sc` string, 
	  `author_sc` string)
	ROW FORMAT SERDE 
	  'org.apache.hadoop.hive.ql.io.orc.OrcSerde' 
	STORED AS INPUTFORMAT 
	  'org.apache.hadoop.hive.ql.io.orc.OrcInputFormat' 
	OUTPUTFORMAT 
	  'org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat'
	LOCATION
	  'hdfs://manager.novalocal:8020/user/hive/warehouse/student4_13.db/citation_data_orc'
	TBLPROPERTIES (
	  'COLUMN_STATS_ACCURATE'='true', 
	  'numFiles'='377', 
	  'numRows'='624183594', 
	  'rawDataSize'='464798785064', 
	  'totalSize'='16119215705', 
    'transient_lastDdlTime'='1592817500')
```


## 2. Заполнить данными из большой таблицы hive_db.citation_data
Данные были заполнены при создании таблицы с помощью:
```sql
CREATE TABLE ...
AS SELECT ...
```
Выполнение данной операции заняло почти 4 часа:
```
INFO  : Total MapReduce CPU Time Spent: 0 dats 3 hours 53 minutes 53 seconds
```
## 3. Посмотреть на получившийся размер данных
[![imageup.ru](https://imageup.ru/img68/3622965/screenshot-from-2020-06-23-15-16-51.png)](https://imageup.ru/img68/3622965/screenshot-from-2020-06-23-15-16-51.png.html)

Размер данных сжался почти в 6.5 раз

## 4. Сделать выводы о эффективности хранения и компресии.
Т.к. полученный размер данных отличается в ощутимое число раз, можно предположить, что команда 
```sql
CREATE TABLE student4_13.citation_data_orc
STORED AS ORC
AS SELECT * FROM hive_db.citation_data;
```
по умолчанию устанавливает 
```SQL 
TBLPROPERTIES ("orc.compress"="SNAPPY")
```
Из-за чего получилось создать таблицу с компрессией, а не без нее, как планировалось.

Также можно предположить, что формат ORC выполняет выравнивание данных, т.к. получилось ровное значение 15.0GB

