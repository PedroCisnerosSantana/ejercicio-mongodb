# ejercicio-mongodb
This repo contains 7 exercises for DB subject

# Create a database
```console
> use ret
switched to db ret
```

# Have a collection
```console
> db.challs.find()
{ "_id" : ObjectId("5e839924f719c57be6b26f8d"), "type" : "rev", "score" : 700, "level" : "real" }
{ "_id" : ObjectId("5e83993cf719c57be6b26f8e"), "type" : "pwn", "score" : 500, "level" : "hard" }
{ "_id" : ObjectId("5e839947f719c57be6b26f8f"), "type" : "web", "score" : 100, "level" : "easy" }
{ "_id" : ObjectId("5e83a1cfd0023dcc9036baed"), "type" : "rev", "score" : 300, "level" : "medium" }
```

# Insert, modify and delete documents in the collection

## Insert
```console
> db.challs.insert({"type" : "crypto", "score" : 300, "level" : "medium"})
```

## Delete
```console
> db.challs.remove({"_id": ObjectId("5e839958f719c57be6b26f90")})
```

## Modify
```console
> var chall = db.challs.findOne({"_id": ObjectId("5e839958f719c57be6b26f90")})
> chall.type = "crypto"
> db.challs.save(chall)
```

# Create index 
```console
> db.challs.createIndex({type: 1})
```

# Make a query using eq, gt, lt

## Query using gt
```console
> db.challs.find({score: {$gt: 299}})
{ "_id" : ObjectId("5e839924f719c57be6b26f8d"), "type" : "rev", "score" : 700, "level" : "real" }
{ "_id" : ObjectId("5e83993cf719c57be6b26f8e"), "type" : "pwn", "score" : 500, "level" : "hard" }
{ "_id" : ObjectId("5e83a1cfd0023dcc9036baed"), "type" : "crypto", "score" : 300, "level" : "medium" }
```

## Query using eq
```console
> db.challs.find({score: {$eq: 700}})
{ "_id" : ObjectId("5e839924f719c57be6b26f8d"), "type" : "rev", "score" : 700, "level" : "real" }
```

## Query using lt
```console
> db.challs.find({score: {$lt: 500}})
{ "_id" : ObjectId("5e839947f719c57be6b26f8f"), "type" : "web", "score" : 100, "level" : "easy" }
{ "_id" : ObjectId("5e83a1cfd0023dcc9036baed"), "type" : "crypto", "score" : 300, "level" : "medium" }
```

# Make a sorted and limited query
```console
> db.challs.find().sort({score: 1}).limit(3)
{ "_id" : ObjectId("5e839947f719c57be6b26f8f"), "type" : "web", "score" : 100, "level" : "easy" }
{ "_id" : ObjectId("5e83a1cfd0023dcc9036baed"), "type" : "crypto", "score" : 300, "level" : "medium" }
{ "_id" : ObjectId("5e83993cf719c57be6b26f8e"), "type" : "pwn", "score" : 500, "level" : "hard" }
```

# Make a grouped query and use a function to show the sum of the values
```console
> db.challs.aggregate( [ { $group: {_id: "$type", Total: {$sum: "$score"} } } ] )
{ "_id" : "crypto", "Total" : 300 }
{ "_id" : "web", "Total" : 100 }
{ "_id" : "pwn", "Total" : 500 }
{ "_id" : "rev", "Total" : 800 }
```
