Switch user
```ruby 
su hadoopusr
```
Input Files 
```ruby 
hadoop fs -mkdir /joininput
hadoopusr@nidhish:/home/nidhish$ hadoop fs -copyFromLocal -f /home/nidhish/Desktop/DeptName.txt /home/nidhish/Desktop/DeptStrength.txt /joininput
```
Program 
```ruby 
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/join$ hadoop jar MapReduceJoin.jar /joininput/DeptName.txt /joininput/DeptStrength.txt /joinoutput
21/06/14 12:13:40 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
21/06/14 12:13:41 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
21/06/14 12:13:41 INFO mapred.FileInputFormat: Total input files to process : 1
21/06/14 12:13:41 INFO mapred.FileInputFormat: Total input files to process : 1
21/06/14 12:13:41 INFO mapreduce.JobSubmitter: number of splits:4
21/06/14 12:13:42 INFO Configuration.deprecation: yarn.resourcemanager.system-metrics-publisher.enabled is deprecated. Instead, use yarn.system-metrics-publisher.enabled
21/06/14 12:13:42 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1623610599748_0003
21/06/14 12:13:43 INFO impl.YarnClientImpl: Submitted application application_1623610599748_0003
21/06/14 12:13:43 INFO mapreduce.Job: The url to track the job: http://nidhish:8088/proxy/application_1623610599748_0003/
21/06/14 12:13:43 INFO mapreduce.Job: Running job: job_1623610599748_0003
21/06/14 12:13:49 INFO mapreduce.Job: Job job_1623610599748_0003 running in uber mode : false
21/06/14 12:13:49 INFO mapreduce.Job:  map 0% reduce 0%
21/06/14 12:14:04 INFO mapreduce.Job:  map 100% reduce 0%
21/06/14 12:14:35 INFO mapreduce.Job:  map 100% reduce 100%
21/06/14 12:14:41 INFO mapreduce.Job: Job job_1623610599748_0003 completed successfully
21/06/14 12:14:42 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=139
                FILE: Number of bytes written=1013326
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=1034
                HDFS: Number of bytes written=85
                HDFS: Number of read operations=15
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=2
        Job Counters 
                Launched map tasks=4
                Launched reduce tasks=1
                Data-local map tasks=4
                Total time spent by all maps in occupied slots (ms)=51806
                Total time spent by all reduces in occupied slots (ms)=24741
                Total time spent by all map tasks (ms)=51806
                Total time spent by all reduce tasks (ms)=24741
                Total vcore-milliseconds taken by all map tasks=51806
                Total vcore-milliseconds taken by all reduce tasks=24741
                Total megabyte-milliseconds taken by all map tasks=53049344
                Total megabyte-milliseconds taken by all reduce tasks=25334784
        Map-Reduce Framework
                Map input records=8
                Map output records=8
                Map output bytes=117
                Map output materialized bytes=157
                Input split bytes=870
                Combine input records=0
                Combine output records=0
                Reduce input groups=4
                Reduce shuffle bytes=157
                Reduce input records=8
                Reduce output records=4
                Spilled Records=16
                Shuffled Maps =4
                Failed Shuffles=0
                Merged Map outputs=4
                GC time elapsed (ms)=264
                CPU time spent (ms)=5940
                Physical memory (bytes) snapshot=1276682240
                Virtual memory (bytes) snapshot=10447892480
                Total committed heap usage (bytes)=970981376
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters 
                Bytes Read=0
        File Output Format Counters 
                Bytes Written=85

```
Output 
```ruby 
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/join$ hadoop fs -ls /joinoutput
Found 2 items
-rw-r--r--   1 hadoopusr supergroup          0 2021-06-14 12:14 /joinoutput/_SUCCESS
-rw-r--r--   1 hadoopusr supergroup         85 2021-06-14 12:14 /joinoutput/part-00000
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/join$ hadoop fs -cat /joinoutput/part-00000
A11     Finance         50
B12     HR              100
C13     Manufacturing           250
Dept_ID Dept_Name               Total_Employee
```

