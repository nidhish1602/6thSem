Input 
```ruby
hadoopusr@nidhish:~$ echo "my name is nidhish and i am studying bda for 6th sem. bda is a very important subject as it provides light on data science and i am interested in it. it includes hadoop, spark, scala, etc. thank you. nidhish, nidhish, nidhish, nidhish, nidhish, very, very, very, very, bda, bda, bda, bda, bda, bda" > input.txt
hadoopusr@nidhish:~$ cat input.txt
my name is nidhish and i am studying bda for 6th sem. bda is a very important subject as it provides light on data science and i am interested in it. it includes hadoop, spark, scala, etc. thank you. nidhish, nidhish, nidhish, nidhish, nidhish, very, very, very, very, bda, bda, bda, bda, bda, bda
```
Output 
```ruby 
scala> val textFile = sc.textFile("/home/hadoopusr/input.txt")
textFile: org.apache.spark.rdd.RDD[String] = /home/hadoopusr/input.txt MapPartitionsRDD[1] at textFile at <console>:24

scala> val counts = textFile.flatMap(line => line.split(" ")).map(word => (word, 1)).reduceByKey((a, b) => a + b)
counts: org.apache.spark.rdd.RDD[(String, Int)] = ShuffledRDD[4] at reduceByKey at <console>:25

scala> import scala.collection.immutable.ListMap
import scala.collection.immutable.ListMap

scala> val sorted=ListMap(counts.collect.sortWith(_._2 > _._2):_*) 
sorted: scala.collection.immutable.ListMap[String,Int] = ListMap(nidhish, -> 5, bda, -> 5, very, -> 4, bda -> 3, is -> 2, am -> 2, it -> 2, i -> 2, and -> 2, provides -> 1, thank -> 1, data -> 1, as -> 1, light -> 1, science -> 1, very -> 1, important -> 1, 6th -> 1, my -> 1, subject -> 1, scala, -> 1, etc. -> 1, includes -> 1, hadoop, -> 1, name -> 1, spark, -> 1, it. -> 1, a -> 1, on -> 1, studying -> 1, sem. -> 1, nidhish -> 1, in -> 1, you. -> 1, for -> 1, interested -> 1)

scala> import scala.collection.immutable.ListMap
import scala.collection.immutable.ListMap

scala> for((k, v)<-sorted)
     | {
     | 
Display all 734 possibilities? (y or n)
     | if(v>4)
     | {
     | print(k+",")
     | print(v)
     | println()
     | }
     | }
nidhish,,5
bda,,5
```
