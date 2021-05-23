# Lab 3 (MongoDB)

1. Create a database “Student” with the following attributes  Rollno, Age, ContactNo, Email-Id.
```ruby
use student
```

2. Insert appropriate values
```ruby
db.user.insert({name:"xyz", rollno: 10, age: 20, contactno: 9898989898, emailid: "xyz@gmail.com"})
WriteResult({ "nInserted" : 1 })
```

```ruby
db.user.insert({name:"abc", rollno: 11, age: 18, contactno: 9898989897, emailid: "pqr@gmail.com"})
WriteResult({ "nInserted" : 1 })
```

3. Write a query to update Email-Id of a student with rollno 10.
```ruby
db.user.update({rollno:10}, {$set:{emailid:"new@gmail.com"}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```

4. Replace the student name from “ABC” to “FEM” of rollno 11.
```ruby
db.user.update({rollno:11}, {$set:{name:"fem"}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```

5. Export the created table into local file system
```ruby
.\mongoexport.exe --db student --collection user --out 'C:\Users\Nidhish Lakhinana\Desktop\info.csv'
2021-04-05T20:31:37.105+0530    connected to: mongodb://localhost/
2021-04-05T20:31:37.118+0530    exported 2 records
```

6. Drop the table
```ruby
> db.user.drop()
true
```

7. Import a given csv dataset from the local file system into mongodb collection.
```ruby
.\mongoimport.exe --db student --collection users 'C:\Users\Nidhish Lakhinana\Desktop\info.csv'
2021-04-06T11:28:36.033+0530    connected to: mongodb://localhost/
2021-04-06T11:28:36.334+0530    2 document(s) imported successfully. 0 document(s) failed to import.
```

8. Print the imported CSV file
```ruby
> db.getCollection('users').find({}).forEach(printjson)
{
        "_id" : ObjectId("606ae33fb67c9a8c34c2ad9c"),
        "name" : "fem",
        "rollno" : 11,
        "age" : 18,
        "contactno" : 9898989897,
        "emailid" : "pqr@gmail.com"
}
{
        "_id" : ObjectId("606ae319b67c9a8c34c2ad9b"),
        "name" : "xyz",
        "rollno" : 10,
        "age" : 20,
        "contactno" : 9898989898,
        "emailid" : "new@gmail.com"
}
```
