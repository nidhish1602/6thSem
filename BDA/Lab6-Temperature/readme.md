Switch to hadoop user 
```ruby
sudo su hadoopusr
```
Start deamons 
```ruby
hadoop-daemon.sh start namenode
starting namenode, logging to /usr/local/hadoop/logs/hadoop-hadoopusr-namenode-nidhish.out

hadoop-daemon.sh start datanode
starting datanode, logging to /usr/local/hadoop/logs/hadoop-hadoopusr-datanode-nidhish.out

yarn-daemon.sh start nodemanager
starting nodemanager, logging to /usr/local/hadoop/logs/yarn-hadoopusr-nodemanager-nidhish.out

yarn-daemon.sh start resourcemanager
starting resourcemanager, logging to /usr/local/hadoop/logs/yarn-hadoopusr-resourcemanager-nidhish.out

jps
30007 DataNode
30823 Jps
30137 NodeManager
29849 NameNode
30333 ResourceManager
```
Create input file
```ruby
hadoopusr@nidhish:/home/nidhish$ hadoop fs -copyFromLocal -f /home/nidhish/Desktop/weatherdataset.txt /tempinput
hadoopusr@nidhish:/home/nidhish$ hadoop fs -ls /tempinput 
Found 2 items
-rw-r--r--   1 hadoopusr supergroup         12 2021-06-14 11:05 /tempinput/input.txt
-rw-r--r--   1 hadoopusr supergroup     888190 2021-06-14 11:25 /tempinput/weatherdataset.txt
```
Run the Java program
```ruby
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/avgtemp$ hadoop jar TemperatureProgram.jar AverageDriver /tempinput/weatherdataset.txt /tempoutput   
21/06/14 11:31:20 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
21/06/14 11:31:20 WARN mapreduce.JobResourceUploader: Hadoop command-line option parsing not performed. Implement the Tool interface and execute your application with ToolRunner to remedy this.
21/06/14 11:31:20 INFO input.FileInputFormat: Total input files to process : 1
21/06/14 11:31:21 INFO mapreduce.JobSubmitter: number of splits:1
21/06/14 11:31:21 INFO Configuration.deprecation: yarn.resourcemanager.system-metrics-publisher.enabled is deprecated. Instead, use yarn.system-metrics-publisher.enabled
21/06/14 11:31:21 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1623610599748_0002
21/06/14 11:31:21 INFO impl.YarnClientImpl: Submitted application application_1623610599748_0002
21/06/14 11:31:21 INFO mapreduce.Job: The url to track the job: http://nidhish:8088/proxy/application_1623610599748_0002/
21/06/14 11:31:21 INFO mapreduce.Job: Running job: job_1623610599748_0002
21/06/14 11:31:28 INFO mapreduce.Job: Job job_1623610599748_0002 running in uber mode : false
21/06/14 11:31:28 INFO mapreduce.Job:  map 0% reduce 0%
21/06/14 11:31:36 INFO mapreduce.Job:  map 100% reduce 0%
21/06/14 11:31:45 INFO mapreduce.Job:  map 100% reduce 100%
21/06/14 11:31:46 INFO mapreduce.Job: Job job_1623610599748_0002 completed successfully
21/06/14 11:31:46 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=72210
                FILE: Number of bytes written=547505
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=888305
                HDFS: Number of bytes written=8
                HDFS: Number of read operations=6
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=2
        Job Counters 
                Launched map tasks=1
                Launched reduce tasks=1
                Data-local map tasks=1
                Total time spent by all maps in occupied slots (ms)=4385
                Total time spent by all reduces in occupied slots (ms)=6032
                Total time spent by all map tasks (ms)=4385
                Total time spent by all reduce tasks (ms)=6032
                Total vcore-milliseconds taken by all map tasks=4385
                Total vcore-milliseconds taken by all reduce tasks=6032
                Total megabyte-milliseconds taken by all map tasks=4490240
                Total megabyte-milliseconds taken by all reduce tasks=6176768
        Map-Reduce Framework
                Map input records=6565
                Map output records=6564
                Map output bytes=59076
                Map output materialized bytes=72210
                Input split bytes=115
                Combine input records=0
                Combine output records=0
                Reduce input groups=1
                Reduce shuffle bytes=72210
                Reduce input records=6564
                Reduce output records=1
                Spilled Records=13128
                Shuffled Maps =1
                Failed Shuffles=0
                Merged Map outputs=1
                GC time elapsed (ms)=35
                CPU time spent (ms)=2070
                Physical memory (bytes) snapshot=490254336
                Virtual memory (bytes) snapshot=4191604736
                Total committed heap usage (bytes)=341835776
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters 
                Bytes Read=888190
        File Output Format Counters 
                Bytes Written=8

```
Output 
```ruby
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/avgtemp$ hadoop fs -ls /tempoutput 
Found 2 items
-rw-r--r--   1 hadoopusr supergroup          0 2021-06-14 11:31 /tempoutput/_SUCCESS
-rw-r--r--   1 hadoopusr supergroup          8 2021-06-14 11:31 /tempoutput/part-r-00000
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/avgtemp$ hadoop fs -cat /tempoutput/part-r-00000
1901    46

```
