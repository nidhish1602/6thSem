### For a given Text file, Create a Map Reduce program to sort the content in an alphabetic order listing only top 10 maximum occurrence of words. ###

1. Switch to hadoop user 
```ruby
sudo su hadoopusr
```
2. cd to hadoop directory
```ruby
cd /usr/local/hadoop/
```
3. Create mapreduce folder
```ruby
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop$ mkdir share
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop$ cd share/
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share$ mkdir hadoop
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share$ cd hadoop/
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop$ mkdir mapreduce
```
4. Start deamons 
```ruby
hadoop-daemon.sh start namenode
starting namenode, logging to /usr/local/hadoop/logs/hadoop-hadoopusr-namenode-nidhish.out
```
```ruby
hadoop-daemon.sh start datanode
starting datanode, logging to /usr/local/hadoop/logs/hadoop-hadoopusr-datanode-nidhish.out
```
```ruby
yarn-daemon.sh start nodemanager
starting nodemanager, logging to /usr/local/hadoop/logs/yarn-hadoopusr-nodemanager-nidhish.out
```
```ruby
yarn-daemon.sh start resourcemanager
starting resourcemanager, logging to /usr/local/hadoop/logs/yarn-hadoopusr-resourcemanager-nidhish.out
```
```ruby
jps
30007 DataNode
30823 Jps
30137 NodeManager
29849 NameNode
30333 ResourceManager
```
5. Read the mapreduce jar file contents
```ruby
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/mapreduce$ hadoop jar MapReduceClient.jar
An example program must be given as the first argument.
Valid program names are:
  aggregatewordcount: An Aggregate based map/reduce program that counts the words in the input files.
  aggregatewordhist: An Aggregate based map/reduce program that computes the histogram of the words in the input files.
  bbp: A map/reduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.
  dbcount: An example job that count the pageview counts from a database.
  distbbp: A map/reduce program that uses a BBP-type formula to compute exact bits of Pi.
  grep: A map/reduce program that counts the matches of a regex in the input.
  join: A job that effects a join over sorted, equally partitioned datasets
  multifilewc: A job that counts words from several files.
  pentomino: A map/reduce tile laying program to find solutions to pentomino problems.
  pi: A map/reduce program that estimates Pi using a quasi-Monte Carlo method.
  randomtextwriter: A map/reduce program that writes 10GB of random textual data per node.
  randomwriter: A map/reduce program that writes 10GB of random data per node.
  secondarysort: An example defining a secondary sort to the reduce.
  sort: A map/reduce program that sorts the data written by the random writer.
  sudoku: A sudoku solver.
  teragen: Generate data for the terasort
  terasort: Run the terasort
  teravalidate: Checking results of terasort
  wordcount: A map/reduce program that counts the words in the input files.
  wordmean: A map/reduce program that counts the average length of the words in the input files.
  wordmedian: A map/reduce program that counts the median length of the words in the input files.
  wordstandarddeviation: A map/reduce program that counts the standard deviation of the length of the words in the input files.
```
6. Create input folder 
```ruby
hadoopusr@nidhish:/home/nidhish$ hadoop fs -mkdir /wcinput
hadoopusr@nidhish:/home/nidhish$ hadoop fs -ls /
Found 6 items
drwxr-xr-x   - hadoopusr supergroup          0 2021-06-13 15:56 /inputfolder
drwxr-xr-x   - hadoopusr supergroup          0 2021-06-13 16:10 /output
drwx------   - hadoopusr supergroup          0 2021-06-09 23:30 /tmp
drwxr-xr-x   - hadoopusr supergroup          0 2021-05-09 20:29 /user
drwxr-xr-x   - hadoopusr supergroup          0 2021-06-14 09:59 /wcinput
drwxr-xr-x   - hadoopusr supergroup          0 2021-06-14 00:48 /weatherinput
```
7. Creating an input file with text 
```ruby
hadoopusr@nidhish:~$ sudo echo "random text" > input.txt 
[sudo] password for hadoopusr: 
hadoopusr@nidhish:~$ hadoop fs -put input.txt /wcinput 
hadoopusr@nidhish:~$ hadoop fs -ls /wcinput
Found 1 items
-rw-r--r--   1 hadoopusr supergroup         12 2021-06-14 10:04 /wcinput/input.txt
```
8. Running WordCount program 
```ruby
hadoopusr@nidhish:~$ cd /usr/local/hadoop/etc/hadoop/share/hadoop/mapreduce
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/mapreduce$ hadoop jar MapReduceClient.jar wordcount /wcinput /wcoutput  
21/06/14 10:07:34 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
21/06/14 10:07:35 INFO input.FileInputFormat: Total input files to process : 1
21/06/14 10:07:35 INFO mapreduce.JobSubmitter: number of splits:1
21/06/14 10:07:35 INFO Configuration.deprecation: yarn.resourcemanager.system-metrics-publisher.enabled is deprecated. Instead, use yarn.system-metrics-publisher.enabled
21/06/14 10:07:36 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1623610599748_0001
21/06/14 10:07:36 INFO impl.YarnClientImpl: Submitted application application_1623610599748_0001
21/06/14 10:07:36 INFO mapreduce.Job: The url to track the job: http://nidhish:8088/proxy/application_1623610599748_0001/
21/06/14 10:07:36 INFO mapreduce.Job: Running job: job_1623610599748_0001
21/06/14 10:07:44 INFO mapreduce.Job: Job job_1623610599748_0001 running in uber mode : false
21/06/14 10:07:44 INFO mapreduce.Job:  map 0% reduce 0%
21/06/14 10:07:49 INFO mapreduce.Job:  map 100% reduce 0%
21/06/14 10:07:55 INFO mapreduce.Job:  map 100% reduce 100%
21/06/14 10:07:55 INFO mapreduce.Job: Job job_1623610599748_0001 completed successfully
21/06/14 10:07:55 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=30
                FILE: Number of bytes written=403997
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=116
                HDFS: Number of bytes written=16
                HDFS: Number of read operations=6
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=2
        Job Counters 
                Launched map tasks=1
                Launched reduce tasks=1
                Data-local map tasks=1
                Total time spent by all maps in occupied slots (ms)=2646
                Total time spent by all reduces in occupied slots (ms)=3195
                Total time spent by all map tasks (ms)=2646
                Total time spent by all reduce tasks (ms)=3195
                Total vcore-milliseconds taken by all map tasks=2646
                Total vcore-milliseconds taken by all reduce tasks=3195
                Total megabyte-milliseconds taken by all map tasks=2709504
                Total megabyte-milliseconds taken by all reduce tasks=3271680
        Map-Reduce Framework
                Map input records=1
                Map output records=2
                Map output bytes=20
                Map output materialized bytes=30
                Input split bytes=104
                Combine input records=2
                Combine output records=2
                Reduce input groups=2
                Reduce shuffle bytes=30
                Reduce input records=2
                Reduce output records=2
                Spilled Records=4
                Shuffled Maps =1
                Failed Shuffles=0
                Merged Map outputs=1
                GC time elapsed (ms)=24
                CPU time spent (ms)=1330
                Physical memory (bytes) snapshot=485306368
                Virtual memory (bytes) snapshot=4185845760
                Total committed heap usage (bytes)=341835776
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters 
                Bytes Read=12
        File Output Format Counters 
                Bytes Written=16
```
9. Output
```ruby
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/mapreduce$ hadoop fs -ls /wcoutput
Found 2 items
-rw-r--r--   1 hadoopusr supergroup          0 2021-06-14 10:07 /wcoutput/_SUCCESS
-rw-r--r--   1 hadoopusr supergroup         16 2021-06-14 10:07 /wcoutput/part-r-00000
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/mapreduce$ hadoop fs -cat /wcoutput/part-r-00000
random  1
text    1
```
