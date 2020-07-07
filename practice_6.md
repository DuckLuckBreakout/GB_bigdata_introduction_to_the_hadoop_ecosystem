# Для части по потоковой обработке (Flume) + HBASE

## Модифицировать свой Flume-фгент, созданный в предыдущем ДЗ таким образом, чтобы данные попадали в HDFS и Hbase одновременно

### Создал таблицу в Hbase:
```
hbase(main):055:0> create 'student4_13', 'data'
0 row(s) in 5.3350 seconds

=> Hbase::Table - student4_13

```

### Добавил Hbase в Configuration File:
```
Flume4_13.sources = ExecSource
Flume4_13.channels = MemChannel HbaseChannel
Flume4_13.sinks = HdfsSink HbaseSink

Flume4_13.sources.ExecSource.type = exec
Flume4_13.sources.ExecSource.channels = MemChannel HbaseChannel
Flume4_13.sources.ExecSource.command = tail -f /tmp/data
Flume4_13.sources.ExecSource.interceptors = i1
Flume4_13.sources.ExecSource.interceptors.i1.type = timestamp

Flume4_13.channels.MemChannel.type = memory
Flume4_13.channels.MemChannel.capacity = 10000

Flume4_13.channels.HbaseChannel.type = memory
Flume4_13.channels.HbaseChannel.capacity = 10000

Flume4_13.sinks.HdfsSink.type = hdfs
Flume4_13.sinks.HdfsSink.channel = MemChannel
Flume4_13.sinks.HdfsSink.hdfs.path = /flume/Flume4_13/%y-%m-%d/
Flume4_13.sinks.HdfsSink.hdfs.filePrefix = -

Flume4_13.sinks.HbaseSink.type = hbase
Flume4_13.sinks.HbaseSink.channel = HbaseChannel
Flume4_13.sinks.HbaseSink.table = student4_13
Flume4_13.sinks.HbaseSink.columnFamily = data
```

### Проверка работоспособности:

#### Дописал `'tst_msg'` в файл `/tmp/data`
```
[student4_13@node1 ~]$ echo "tst_msg" >> /tmp/data
```
##### Проверка изменения в `/flume/Flume4_13/%y-%m-%d/`:
```
[student4_13@node1 ~]$ hdfs dfs -ls /flume/Flume4_13/20-07-07/
Found 11 items
-rw-r--r--   3 flume flume        355 2020-07-07 11:14 /flume/Flume4_13/20-07-07/-.1594120427458
-rw-r--r--   3 flume flume        207 2020-07-07 11:15 /flume/Flume4_13/20-07-07/-.1594120477545
-rw-r--r--   3 flume flume        187 2020-07-07 11:15 /flume/Flume4_13/20-07-07/-.1594120511083
-rw-r--r--   3 flume flume        367 2020-07-07 11:18 /flume/Flume4_13/20-07-07/-.1594120700499
-rw-r--r--   3 flume flume        415 2020-07-07 11:20 /flume/Flume4_13/20-07-07/-.1594120817107
-rw-r--r--   3 flume flume        359 2020-07-07 11:20 /flume/Flume4_13/20-07-07/-.1594120817108
-rw-r--r--   3 flume flume        142 2020-07-07 11:28 /flume/Flume4_13/20-07-07/-.1594121269928
-rw-r--r--   3 flume flume        355 2020-07-07 10:52 /flume/Flume4_13/20-07-07/events.1594119106049
-rw-r--r--   3 flume flume        139 2020-07-07 10:54 /flume/Flume4_13/20-07-07/events.1594119246393
-rw-r--r--   3 flume flume        355 2020-07-07 11:00 /flume/Flume4_13/20-07-07/events.1594119605001
-rw-r--r--   3 flume flume        207 2020-07-07 11:01 /flume/Flume4_13/20-07-07/events.1594119645131
```
Проверка самого молодого файла:
```
[student4_13@node1 ~]$ hdfs dfs -cat /flume/Flume4_13/20-07-07/-.1594121269928
SEQ!org.apache.hadoop.io.LongWritable"org.apache.hadoop.io.BytesWritable�@�c&�o���
                                                                                    �7s2�tst_msg�����@�c&�o���
                                                                                                                �7
```
`'tst_msg'` записано

##### Проверка изменения в Hbase:
```
hbase(main):001:0> scan 'student4_13'
ROW                                     COLUMN+CELL                                                                                                      
 default8c7b412e-969a-4fb0-9365-304de58 column=data:pCol, timestamp=1594121277685, value=tst_msg                                                         
 4b2fd                                                                                                                                                   
 incRow                                 column=data:iCol, timestamp=1594121277692, value=\x00\x00\x00\x00\x00\x00\x00\x01                                
2 row(s) in 0.6050 seconds
```
`'tst_msg'` записано
