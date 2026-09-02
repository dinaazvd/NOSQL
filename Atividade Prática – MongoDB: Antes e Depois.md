# Prática MongoDb
```db.customers.find({"name": "Ana"}, {"name":1, "city":2})
db.customers.find({"name": "Carlos"}, {"name":1, "city":2})```
Nao aparece o ID quando executa
`({"name": "Carlos"}, {"_id": 0, "name":1, "city":2})`

Ex 2
 db.customers.updateOne({"name": "Carlos"}, {$set:{"active": "true"}})

Ex3
 db.customers.updateMany({"city": "Salvador"}, {$set:{"state": "BA"}})
Ex 4
 db.customers.updateMany({"name": "Ana"}, {$inc:{"points": 50}})
Ex 5
 db.customers.insertOne({
   "name": "Fernando",
   "age": 29,
   "city": "Recife",
   "active": true,
   "points": 90 })
Ex 6 
db.customers.deleteOne({"name": "Eduarda"})
Ex 7
 db.customers.updateOne({"name": "Daniela"}, {$set:{"vip": true}})
Ex 8
db.customers.updateOne({"name": "Bruno"},{$unset: {"points": 300}} )
Ex 9

