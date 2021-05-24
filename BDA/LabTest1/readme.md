# Lab test 1

### Using MongoDB
i)Create a mongodb collection Hospital by choosing appropriate attributes
```ruby 
> use hospital
switched to db hospital
```
ii) Insert three documents
```ruby 
> db.admin.insert({name:"nidhish", age:20, phoneno: 9849400000, dept: "ENT"})
WriteResult({ "nInserted" : 1 })
> db.admin.insert({name:"krishna", age:35, phoneno: 7200019124, dept: "Dermatologist"})
WriteResult({ "nInserted" : 1 })
> db.admin.insert({name:"akshay", age:29, phoneno: 6300142391, dept: "cardiologist"})
WriteResult({ "nInserted" : 1 })
```
iii) List all the documents
```ruby 
> db.admin.find()
{ "_id" : ObjectId("60ab71e44618ad6e35580371"), "name" : "nidhish", "age" : 20, "phoneno" : 9849400000, "dept" : "ENT" }
{ "_id" : ObjectId("60ab72a24618ad6e35580372"), "name" : "krishna", "age" : 35, "phoneno" : 7200019124, "dept" : "Dermatologist" }
{ "_id" : ObjectId("60ab72a74618ad6e35580373"), "name" : "akshay", "age" : 29, "phoneno" : 6300142391, "dept" : "cardiologist" }
> db.admin.find().pretty()
{
        "_id" : ObjectId("60ab71e44618ad6e35580371"),
        "name" : "nidhish",
        "age" : 20,
        "phoneno" : 9849400000,
        "dept" : "ENT"
}
{
        "_id" : ObjectId("60ab72a24618ad6e35580372"),
        "name" : "krishna",
        "age" : 35,
        "phoneno" : 7200019124,
        "dept" : "Dermatologist"
}
{
        "_id" : ObjectId("60ab72a74618ad6e35580373"),
        "name" : "akshay",
        "age" : 29,
        "phoneno" : 6300142391,
        "dept" : "cardiologist"
}
```
iv)Demonstrate update operation
```ruby 
> db.admin.update({phoneno:9849400000}, {$set:{age:21}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.admin.find()
{ "_id" : ObjectId("60ab71e44618ad6e35580371"), "name" : "nidhish", "age" : 21, "phoneno" : 9849400000, "dept" : "ENT" }
{ "_id" : ObjectId("60ab72a24618ad6e35580372"), "name" : "krishna", "age" : 35, "phoneno" : 7200019124, "dept" : "Dermatologist" }
{ "_id" : ObjectId("60ab72a74618ad6e35580373"), "name" : "akshay", "age" : 29, "phoneno" : 6300142391, "dept" : "cardiologist" }
```


### Using CQL write queries for the following:
i) Create a Keyspace Company and Create the Column Family
Customer(Customerid, Customername, Item_Purchased, City,Date)
```ruby 
cqlsh> use company;
cqlsh:company> create table customer(customerid int, customername text,
           ... item_purchased text, city text, date timestamp, 
           ... primary key(customerid));
```
ii) Insert required row to the Column Family.
```ruby 
cqlsh:company> insert into customer (customerid, customername, item_purchased, city, date)
           ... values (01, 'Akshay', 'iPhone 12', 'Bangalore', '2021-05-10');
cqlsh:company> insert into customer (customerid, customername, item_purchased, city, date)
           ... values (02, 'Shreya', 'Oneplus 6', 'Delhi', '2021-01-22');
cqlsh:company> insert into customer (customerid, customername, item_purchased, city, date)
           ... values (03, 'Nidhish', 'Pixel 5', 'Bangalore', '2021-03-12');
cqlsh:company> insert into customer (customerid, customername, item_purchased, city, date)
           ... values (04, 'Kartik', 'iPhone 11', 'Mumbai', '2021-04-01');
cqlsh:company> select * from customer;

 customerid | city      | customername | date                            | item_purchased
------------+-----------+--------------+---------------------------------+----------------
          1 | Bangalore |       Akshay | 2021-05-09 18:30:00.000000+0000 |      iPhone 12
          2 |     Delhi |       Shreya | 2021-01-21 18:30:00.000000+0000 |      Oneplus 6
          4 |    Mumbai |       Kartik | 2021-03-31 18:30:00.000000+0000 |      iPhone 11
          3 | Bangalore |      Nidhish | 2021-03-11 18:30:00.000000+0000 |        Pixel 5
```
iii) Display Customername and Item_Purchased whose city is “Bangalore” from date 1/5/2021 to till date.
```ruby 
cqlsh:company> select customername, item_purchased from customer where
           ... city = 'Bangalore' and  date >= '2021-05-01' allow filtering;

 customername | item_purchased
--------------+----------------
       Akshay |      iPhone 12
```
iv) Add new field “Customer_Feedback” with Value “Good” to the row (_id:4) ofColumn Family.
```ruby 
cqlsh:company> alter table customer add customer_feedback text;
cqlsh:company> update customer set customer_feedback = 'Good' where customerid = 04;
cqlsh:company> select * from customer;

 customerid | city      | customer_feedback | customername | date                            | item_purchased
------------+-----------+-------------------+--------------+---------------------------------+----------------
          1 | Bangalore |              null |       Akshay | 2021-05-09 18:30:00.000000+0000 |      iPhone 12
          2 |     Delhi |              null |       Shreya | 2021-01-21 18:30:00.000000+0000 |      Oneplus 6
          4 |    Mumbai |              Good |       Kartik | 2021-03-31 18:30:00.000000+0000 |      iPhone 11
          3 | Bangalore |              null |      Nidhish | 2021-03-11 18:30:00.000000+0000 |        Pixel 5
```
v)Import an existing csv file into the current column family. (Made a copy of the existing database and added a row)
```ruby 
cqlsh:company> copy customer (customerid, customername, item_purchased, city, date, customer_feedback) to 'sample.csv';       
Using 7 child processes

Starting copy of company.customer with columns [customerid, customername, item_purchased, city, date, customer_feedback].
cqlshlib.copyutil.ExportProcess.write_rows_to_csv(): writing row
cqlshlib.copyutil.ExportProcess.write_rows_to_csv(): writing row
cqlshlib.copyutil.ExportProcess.write_rows_to_csv(): writing row
cqlshlib.copyutil.ExportProcess.write_rows_to_csv(): writing row
Processed: 4 rows; Rate:      90 rows/s; Avg. rate:      10 rows/s
4 rows exported to 1 files in 0.429 seconds.
cqlsh:company> select * from customer;

 customerid | city      | customer_feedback | customername | date                            | item_purchased
------------+-----------+-------------------+--------------+---------------------------------+----------------
          1 | Bangalore |              null |       Akshay | 2021-05-09 18:30:00.000000+0000 |      iPhone 12
          2 |     Delhi |              null |       Shreya | 2021-01-21 18:30:00.000000+0000 |      Oneplus 6
          4 |    Mumbai |              Good |       Kartik | 2021-03-31 18:30:00.000000+0000 |      iPhone 11
          3 | Bangalore |              null |      Nidhish | 2021-03-11 18:30:00.000000+0000 |        Pixel 5


cqlsh:company> copy customer (customerid, customername, item_purchased, city, date, customer_feedback) from 'sample.csv';
Using 7 child processes

Starting copy of company.customer with columns [customerid, customername, item_purchased, city, date, customer_feedback].
Processed: 5 rows; Rate:       5 rows/s; Avg. rate:       6 rows/s
5 rows imported from 1 files in 0.852 seconds (0 skipped).
cqlsh:company> select * from customer;

 customerid | city      | customer_feedback | customername | date                            | item_purchased
------------+-----------+-------------------+--------------+---------------------------------+----------------
          5 | Bangalore |              null |      Chaahel | 2021-03-12 18:30:00.000000+0000 |        Pixel 4
          1 | Bangalore |              null |       Akshay | 2021-05-09 18:30:00.000000+0000 |      iPhone 12
          2 |     Delhi |              null |       Shreya | 2021-01-21 18:30:00.000000+0000 |      Oneplus 6
          4 |    Mumbai |              Good |       Kartik | 2021-03-31 18:30:00.000000+0000 |      iPhone 11
          3 | Bangalore |              null |      Nidhish | 2021-03-11 18:30:00.000000+0000 |        Pixel 5

```
