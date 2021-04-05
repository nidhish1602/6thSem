use student

db.user.insert({rollno: 1, age: 20, contactno: 9898989898, emailid: "xyz@gmail.com"})

db.user.insert({name:"xyz", rollno: 10, age: 20, contactno: 9898989898, emailid: "xyz@gmail.com"})
WriteResult({ "nInserted" : 1 })

db.user.insert({name:"abc", rollno: 11, age: 18, contactno: 9898989897, emailid: "pqr@gmail.com"})
WriteResult({ "nInserted" : 1 })

db.user.update({rollno:10}, {$set:{emailid:"new@gmail.com"}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

db.user.update({rollno:11}, {$set:{name:"fem"}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

.\mongoexport.exe --db student --collection user --out 'C:\Users\Nidhish Lakhinana\Desktop\info.csv'
2021-04-05T20:31:37.105+0530    connected to: mongodb://localhost/
2021-04-05T20:31:37.118+0530    exported 2 records
