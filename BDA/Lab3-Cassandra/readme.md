# Lab 3 (Cassandra)

## Create a library information database

```ruby 
cqlsh> create keyspace library_info with replication =
   ... {'class':'SimpleStrategy','replication_factor':1};
```

```ruby 
cqlsh> use library_info;
```

```ruby 
cqlsh:library_info> create table library_details(stud_id int,counter_value
                ... counter,stud_name text,book_name text,date_of_issue timestamp,book_id
                ... int,primary key(stud_id,stud_name,book_name,date_of_issue,book_id));

```

```ruby 
cqlsh:library_info> update library_details set counter_value=counter_value+1
                ... where stud_id=111 and stud_name='shreya' and book_name='ML' and    
                ... date_of_issue='2020-11-09' and book_id=200;
cqlsh:library_info> update library_details set counter_value=counter_value+1
                ... where stud_id=112 and stud_name='jhanvi' and book_name='BDA' and       
                ... date_of_issue='2020-01-01' and book_id=300;
cqlsh:library_info> update library_details set counter_value=counter_value+1
                ... where stud_id=113 and stud_name='akshaya' and book_name='OOMD' and        
                ... date_of_issue='2020-06-01' and book_id=400;

```

```ruby 
cqlsh:library_info> select * from library_details;

 stud_id | stud_name | book_name | date_of_issue                   | book_id | counter_value
---------+-----------+-----------+---------------------------------+---------+---------------
     111 |    shreya |        ML | 2020-11-08 18:30:00.000000+0000 |     200 |             1
     113 |   akshaya |      OOMD | 2020-05-31 18:30:00.000000+0000 |     400 |             1
     112 |    jhanvi |       BDA | 2019-12-31 18:30:00.000000+0000 |     300 |             1
```

```ruby 
cqlsh:library_info> update library_details set counter_value=counter_value+1
                ... where stud_id=112 and stud_name='jhanvi' and book_name='BDA' and
                ... date_of_issue='2020-01-01' and book_id=300;
cqlsh:library_info> select * from library_details where stud_id=112;

 stud_id | stud_name | book_name | date_of_issue                   | book_id | counter_value
---------+-----------+-----------+---------------------------------+---------+---------------
     112 |    jhanvi |       BDA | 2019-12-31 18:30:00.000000+0000 |     300 |             2

```

```ruby 
cqlsh:library_info> copy
                ... library_details(stud_id,stud_name,book_name,book_id,date_of_issue,counter_value)
                ... to '/home/nidhish/Desktop/librarydb.csv';
Using 7 child processes

Starting copy of library_info.library_details with columns [stud_id, stud_name, book_name, book_id, date_of_issue, counter_value].
cqlshlib.copyutil.ExportProcess.write_rows_to_csv(): writing row
cqlshlib.copyutil.ExportProcess.write_rows_to_csv(): writing row
cqlshlib.copyutil.ExportProcess.write_rows_to_csv(): writing row
Processed: 3 rows; Rate:      12 rows/s; Avg. rate:      12 rows/s
3 rows exported to 1 files in 0.277 seconds.

```

```ruby 
cqlsh:library_info> select * from library_details;

 stud_id | stud_name | book_name | date_of_issue                   | book_id | counter_value
---------+-----------+-----------+---------------------------------+---------+---------------
     111 |    shreya |        ML | 2020-11-08 18:30:00.000000+0000 |     200 |             1
     113 |   akshaya |      OOMD | 2020-05-31 18:30:00.000000+0000 |     400 |             1
     112 |    jhanvi |       BDA | 2019-12-31 18:30:00.000000+0000 |     300 |             2

```

