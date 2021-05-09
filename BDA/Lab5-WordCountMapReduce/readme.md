###For a given Text file, Create a Map Reduce program to sort the content in an alphabetic order listing only top 10 maximum occurrence of words.###

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
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/mapreduce$ hadoop-daemon.sh start datanode
starting datanode, logging to /usr/local/hadoop/logs/hadoop-hadoopusr-datanode-nidhish.out
```
```ruby
yarn-daemon.sh start nodemanager
starting nodemanager, logging to /usr/local/hadoop/logs/yarn-hadoopusr-nodemanager-nidhish.out
```
```ruby
yarn-daemon.sh start resourcemanager
starting resourcemanager, logging to /usr/local/hadoop/logs/yarn-hadoopusr-resourcemanager-nidhish.out```
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
6. Create directory in HDFS
```ruby
hadoopusr@nidhish:/usr/local/hadoop/etc/hadoop/share/hadoop/mapreduce$ hadoop fs -mkdir -p input
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.apache.hadoop.security.authentication.util.KerberosUtil (file:/usr/local/hadoop/share/hadoop/common/lib/hadoop-auth-2.9.0.jar) to method sun.security.krb5.Config.getInstance()
WARNING: Please consider reporting this to the maintainers of org.apache.hadoop.security.authentication.util.KerberosUtil
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
21/05/09 20:29:20 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
```
