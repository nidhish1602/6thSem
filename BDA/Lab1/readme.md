# Lab 1 

## Cassandra sample program

```ruby
cqlsh> create keyspace students with
   ... replication={'class':'SimpleStrategy','replication_factor':1}; 
```

```ruby
cqlsh> use students;
```
 
Check if the keyspace is created
```ruby
cqlsh:students> describe keyspaces
```

```ruby
cqlsh:students> create table student_profile(rollno int primary key,studname
            ... text,dateofjoining timestamp,lastexampercent int);
```

See the table 'student_profile' schema
```ruby
DESCRIBE TABLE student_profile;

CREATE TABLE students.student_profile (
    rollno int PRIMARY KEY,
    dateofjoining timestamp,
    lastexampercent int,
    studname text
) WITH additional_write_policy = '99p'
    AND bloom_filter_fp_chance = 0.01
    AND caching = {'keys': 'ALL', 'rows_per_partition': 'NONE'}
    AND cdc = false
    AND comment = ''
    AND compaction = {'class': 'org.apache.cassandra.db.compaction.SizeTieredCompactionStrategy', 'max_threshold': '32', 'min_threshold': '4'}
    AND compression = {'chunk_length_in_kb': '16', 'class': 'org.apache.cassandra.io.compress.LZ4Compressor'}
    AND crc_check_chance = 1.0
    AND default_time_to_live = 0
    AND extensions = {}
    AND gc_grace_seconds = 864000
    AND max_index_interval = 2048
    AND memtable_flush_period_in_ms = 0
    AND min_index_interval = 128
    AND read_repair = 'BLOCKING'
    AND speculative_retry = '99p';
```

```ruby
cqlsh:students> select * from student_profile;

 rollno | dateofjoining                   | lastexampercent | studname
--------+---------------------------------+-----------------+----------
      1 | 2020-10-09 18:30:00.000000+0000 |              89 |      sam
      2 | 2020-09-08 18:30:00.000000+0000 |              88 |    tanya
```

```ruby
cqlsh:students> update student_profile set studname='nikil' where rollno=2;     
cqlsh:students> select * from student_profile;

 rollno | dateofjoining                   | lastexampercent | studname
--------+---------------------------------+-----------------+----------
      1 | 2020-10-09 18:30:00.000000+0000 |              89 |      sam
      2 | 2020-09-08 18:30:00.000000+0000 |              88 |    nikil
```

```ruby
cqlsh:students> select * from student_profile where rollno in (2);

 rollno | dateofjoining                   | lastexampercent | studname
--------+---------------------------------+-----------------+----------
      2 | 2020-09-08 18:30:00.000000+0000 |              88 |    nikil
```

```ruby
cqlsh:students> create index on student_profile(studname);
cqlsh:students> select rollno,lastexampercent from student_profile where
            ... studname='nikil';

 rollno | lastexampercent
--------+-----------------
      2 |              88
```

```ruby
cqlsh:students> select rollno,lastexampercent from student_profile limit 1;

 rollno | lastexampercent
--------+-----------------
      1 |              89
```

```ruby
cqlsh:students> select rollno, studname as "name" from student_profile;

 rollno | name
--------+-------
      1 |   sam
      2 | nikil
```

```ruby
cqlsh:students> delete lastexampercent from student_profile where rollno=1;
cqlsh:students> select * from student_profile;

 rollno | dateofjoining                   | lastexampercent | studname
--------+---------------------------------+-----------------+----------
      1 | 2020-10-09 18:30:00.000000+0000 |            null |      sam
      2 | 2020-09-08 18:30:00.000000+0000 |              88 |    nikil
```

```ruby
cqlsh:students> delete from student_profile where rollno=1;
cqlsh:students> select * from student_profile;

 rollno | dateofjoining                   | lastexampercent | studname
--------+---------------------------------+-----------------+----------
      2 | 2020-09-08 18:30:00.000000+0000 |              88 |    nikil

```

