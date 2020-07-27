# Практическое задание к лекции по YARN
## 0. [Исследовательское задание]
Как получить доступ под пользователем hdfs в файловую систему не имея sudo?
```console
[student4_13@manager ~]$ export HADOOP_USER_NAME=hdfs
```

## 1. Опробовать запуски map-reduce задач для кластера используя hadoop-mapreduce-examples.jar.
```console
[student4_13@manager ~]$ export YARN_EXAMPLES=/opt/cloudera/parcels/CDH-5.16.2-1.cdh5.16.2.p0.8/lib/hadoop-mapreduce
```
### а. Выполнить три любых задачи включенных в этот JAR.

```console
[student4_13@node3 ~]$ yarn jar $YARN_EXAMPLES/hadoop-mapreduce-examples.jar pi 32 20000
Number of Maps  = 32
Samples per Map = 20000
Wrote input for Map #0
Wrote input for Map #1
Wrote input for Map #2
Wrote input for Map #3
Wrote input for Map #4
Wrote input for Map #5
Wrote input for Map #6
Wrote input for Map #7
Wrote input for Map #8
Wrote input for Map #9
Wrote input for Map #10
Wrote input for Map #11
Wrote input for Map #12
Wrote input for Map #13
Wrote input for Map #14
Wrote input for Map #15
Wrote input for Map #16
Wrote input for Map #17
Wrote input for Map #18
Wrote input for Map #19
Wrote input for Map #20
Wrote input for Map #21
Wrote input for Map #22
Wrote input for Map #23
Wrote input for Map #24
Wrote input for Map #25
Wrote input for Map #26
Wrote input for Map #27
Wrote input for Map #28
Wrote input for Map #29
Wrote input for Map #30
Wrote input for Map #31
Starting Job
20/07/27 17:06:07 INFO client.RMProxy: Connecting to ResourceManager at manager.novalocal/89.208.221.132:8032
20/07/27 17:06:09 INFO input.FileInputFormat: Total input paths to process : 32
20/07/27 17:06:09 INFO mapreduce.JobSubmitter: number of splits:32
20/07/27 17:06:09 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1593546320308_0242
20/07/27 17:06:10 INFO impl.YarnClientImpl: Submitted application application_1593546320308_0242
20/07/27 17:06:10 INFO mapreduce.Job: The url to track the job: http://manager.novalocal:8088/proxy/application_1593546320308_0242/
20/07/27 17:06:10 INFO mapreduce.Job: Running job: job_1593546320308_0242
20/07/27 17:06:35 INFO mapreduce.Job: Job job_1593546320308_0242 running in uber mode : false
20/07/27 17:06:35 INFO mapreduce.Job:  map 0% reduce 0%
20/07/27 17:06:49 INFO mapreduce.Job:  map 31% reduce 0%
20/07/27 17:06:50 INFO mapreduce.Job:  map 44% reduce 0%
20/07/27 17:06:53 INFO mapreduce.Job:  map 47% reduce 0%
20/07/27 17:06:56 INFO mapreduce.Job:  map 50% reduce 0%
20/07/27 17:06:57 INFO mapreduce.Job:  map 69% reduce 0%
20/07/27 17:07:15 INFO mapreduce.Job:  map 81% reduce 0%
20/07/27 17:07:23 INFO mapreduce.Job:  map 97% reduce 0%
20/07/27 17:07:34 INFO mapreduce.Job:  map 97% reduce 32%
20/07/27 17:07:43 INFO mapreduce.Job:  map 100% reduce 32%
20/07/27 17:07:46 INFO mapreduce.Job:  map 100% reduce 100%
20/07/27 17:09:22 INFO mapreduce.Job: Job job_1593546320308_0242 completed successfully
20/07/27 17:09:22 INFO mapreduce.Job: Counters: 50
	File System Counters
		FILE: Number of bytes read=264
		FILE: Number of bytes written=4943563
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=8662
		HDFS: Number of bytes written=215
		HDFS: Number of read operations=131
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=3
	Job Counters 
		Launched map tasks=32
		Launched reduce tasks=1
		Data-local map tasks=31
		Rack-local map tasks=1
		Total time spent by all maps in occupied slots (ms)=2042180
		Total time spent by all reduces in occupied slots (ms)=183172
		Total time spent by all map tasks (ms)=510545
		Total time spent by all reduce tasks (ms)=45793
		Total vcore-milliseconds taken by all map tasks=510545
		Total vcore-milliseconds taken by all reduce tasks=45793
		Total megabyte-milliseconds taken by all map tasks=522798080
		Total megabyte-milliseconds taken by all reduce tasks=46892032
	Map-Reduce Framework
		Map input records=32
		Map output records=64
		Map output bytes=576
		Map output materialized bytes=1120
		Input split bytes=4886
		Combine input records=0
		Combine output records=0
		Reduce input groups=2
		Reduce shuffle bytes=1120
		Reduce input records=64
		Reduce output records=0
		Spilled Records=128
		Shuffled Maps =32
		Failed Shuffles=0
		Merged Map outputs=32
		GC time elapsed (ms)=6252
		CPU time spent (ms)=39670
		Physical memory (bytes) snapshot=14582202368
		Virtual memory (bytes) snapshot=92209942528
		Total committed heap usage (bytes)=14406385664
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=3776
	File Output Format Counters 
		Bytes Written=97
Job Finished in 194.791 seconds
Estimated value of Pi is 3.14153125000000000000

```

```console
[student4_13@node3 ~]$ yarn jar $YARN_EXAMPLES/hadoop-mapreduce-examples.jar wordcount /tmp/test.py /tmp/test_py_wc
20/07/27 17:49:52 INFO client.RMProxy: Connecting to ResourceManager at manager.novalocal/89.208.221.132:8032
20/07/27 17:49:53 INFO input.FileInputFormat: Total input paths to process : 1
20/07/27 17:49:53 INFO mapreduce.JobSubmitter: number of splits:1
20/07/27 17:49:53 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1593546320308_0255
20/07/27 17:49:54 INFO impl.YarnClientImpl: Submitted application application_1593546320308_0255
20/07/27 17:49:54 INFO mapreduce.Job: The url to track the job: http://manager.novalocal:8088/proxy/application_1593546320308_0255/
20/07/27 17:49:54 INFO mapreduce.Job: Running job: job_1593546320308_0255
20/07/27 17:50:01 INFO mapreduce.Job: Job job_1593546320308_0255 running in uber mode : false
20/07/27 17:50:01 INFO mapreduce.Job:  map 0% reduce 0%
20/07/27 17:50:07 INFO mapreduce.Job:  map 100% reduce 0%
20/07/27 17:50:13 INFO mapreduce.Job:  map 100% reduce 33%
20/07/27 17:50:16 INFO mapreduce.Job:  map 100% reduce 83%
20/07/27 17:50:24 INFO mapreduce.Job:  map 100% reduce 100%
20/07/27 17:50:24 INFO mapreduce.Job: Job job_1593546320308_0255 completed successfully
20/07/27 17:50:24 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=314
		FILE: Number of bytes written=1046362
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=226
		HDFS: Number of bytes written=137
		HDFS: Number of read operations=21
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=12
	Job Counters 
		Launched map tasks=1
		Launched reduce tasks=6
		Rack-local map tasks=1
		Total time spent by all maps in occupied slots (ms)=13484
		Total time spent by all reduces in occupied slots (ms)=160332
		Total time spent by all map tasks (ms)=3371
		Total time spent by all reduce tasks (ms)=40083
		Total vcore-milliseconds taken by all map tasks=3371
		Total vcore-milliseconds taken by all reduce tasks=40083
		Total megabyte-milliseconds taken by all map tasks=3451904
		Total megabyte-milliseconds taken by all reduce tasks=41044992
	Map-Reduce Framework
		Map input records=6
		Map output records=17
		Map output bytes=184
		Map output materialized bytes=290
		Input split bytes=106
		Combine input records=17
		Combine output records=15
		Reduce input groups=15
		Reduce shuffle bytes=290
		Reduce input records=15
		Reduce output records=15
		Spilled Records=30
		Shuffled Maps =6
		Failed Shuffles=0
		Merged Map outputs=6
		GC time elapsed (ms)=843
		CPU time spent (ms)=7370
		Physical memory (bytes) snapshot=1743245312
		Virtual memory (bytes) snapshot=19645288448
		Total committed heap usage (bytes)=1563951104
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=120
	File Output Format Counters 
		Bytes Written=137
```
```console
[student4_13@node3 ~]$ yarn jar $YARN_EXAMPLES/hadoop-mapreduce-examples.jar sudoku sudoku.txt
Solving sudoku.txt
8 5 1 3 9 2 6 4 7 
4 3 2 6 7 8 1 9 5 
7 9 6 5 1 4 3 8 2 
6 1 4 8 2 3 7 5 9 
5 7 8 9 6 1 4 2 3 
3 2 9 4 5 7 8 1 6 
9 4 7 2 8 6 5 3 1 
1 8 5 7 3 9 2 6 4 
2 6 3 1 4 5 9 7 8 

Found 1 solutions

```
### б. Найти свои задачи в интерфейсе Cloudera Manager
[![imageup.ru](https://imageup.ru/img109/3635612/screenshot-from-2020-07-27-20-06-55.png)](https://imageup.ru/img109/3635612/screenshot-from-2020-07-27-20-06-55.png.html)
[![imageup.ru](https://imageup.ru/img130/3635617/screenshot-from-2020-07-27-20-50-22.png)](https://imageup.ru/img130/3635617/screenshot-from-2020-07-27-20-50-22.png.html)
### в. Опробовать навигацию по интерфейсу YARN


