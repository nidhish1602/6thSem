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

```ruby
x
```
