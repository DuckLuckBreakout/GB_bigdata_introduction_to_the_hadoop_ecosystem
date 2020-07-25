# Практическое задание к лекции по YARN
## 0. [Исследовательское задание]
Как получить доступ под пользователем hdfs в файловую систему не имея sudo?
```console
[student4_13@manager ~]$ export HADOOP_USER_NAME=hdfs
```

### Опробовать запуски map-reduce задач для кластера используя hadoop-mapreduce-examples.jar.
```console
[student4_13@manager ~]$ export YARN_EXAMPLES=/opt/cloudera/parcels/CDH-5.16.2-1.cdh5.16.2.p0.8/lib/hadoop-mapreduce
```
а. Выполнить три любых задачи включенных в этот JAR.

```console
[student4_13@manager ~]$ yarn jar $YARN_EXAMPLES/hadoop-mapreduce-examples.jar pi 32 20000
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
20/07/25 19:05:07 INFO client.RMProxy: Connecting to ResourceManager at manager.novalocal/89.208.221.132:8032
20/07/25 19:05:08 INFO input.FileInputFormat: Total input paths to process : 32
20/07/25 19:05:08 INFO mapreduce.JobSubmitter: number of splits:32
20/07/25 19:05:10 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1593546320308_0239
20/07/25 19:05:10 INFO impl.YarnClientImpl: Submitted application application_1593546320308_0239
20/07/25 19:05:10 INFO mapreduce.Job: The url to track the job: http://manager.novalocal:8088/proxy/application_1593546320308_0239/
20/07/25 19:05:10 INFO mapreduce.Job: Running job: job_1593546320308_0239
20/07/25 19:05:28 INFO mapreduce.Job: Job job_1593546320308_0239 running in uber mode : false
20/07/25 19:05:28 INFO mapreduce.Job:  map 0% reduce 0%
20/07/25 19:05:41 INFO mapreduce.Job:  map 13% reduce 0%
20/07/25 19:06:23 INFO mapreduce.Job:  map 19% reduce 0%
20/07/25 19:06:25 INFO mapreduce.Job:  map 22% reduce 0%
20/07/25 19:06:27 INFO mapreduce.Job:  map 38% reduce 0%
20/07/25 19:06:28 INFO mapreduce.Job:  map 44% reduce 0%
20/07/25 19:06:29 INFO mapreduce.Job:  map 53% reduce 0%
20/07/25 19:06:30 INFO mapreduce.Job:  map 59% reduce 0%
20/07/25 19:06:33 INFO mapreduce.Job:  map 72% reduce 0%
20/07/25 19:06:42 INFO mapreduce.Job:  map 75% reduce 0%
20/07/25 19:06:43 INFO mapreduce.Job:  map 78% reduce 0%
20/07/25 19:06:44 INFO mapreduce.Job:  map 84% reduce 0%
20/07/25 19:07:01 INFO mapreduce.Job:  map 84% reduce 28%
20/07/25 19:07:02 INFO mapreduce.Job:  map 91% reduce 28%
20/07/25 19:07:07 INFO mapreduce.Job:  map 91% reduce 30%
20/07/25 19:07:15 INFO mapreduce.Job:  map 100% reduce 30%

```
б. Найти свои задачи в интерфейсе Cloudera Manager

в. Опробовать навигацию по интерфейсу YARN
