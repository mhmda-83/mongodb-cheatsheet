# Show list of databases

`show databases` OR `show dbs`

# Show list of collections

`show collections`

# Create or switch between databases

`use database_name`

# Create collection

`db.createCollection('collection_name')`

# insert document

you can define variable (js syntax) and pass it as excepted parameter.

```javascript
var user = {
  name: "Mohammad MohammadAlian",
  ip: "127.0.0.1",
  lastLoginTime: 1575704736
};

db.insertOne(user);
```

OR

`db.collection.insertOne({name: 'Mohammad MohammadAlian', ip: '127.0.0.1', lastLoginTime: 1575704736})`;

to insert many object in one query you can use insertMany function

```javascript
var users = [
  {
    name: "Mohammad MohammadAlian",
    ip: "127.0.0.1",
    lastLoginTime: 1575704736
  },
  { name: "John Doe", ip: "10.10.10.10", lastLoginTime: 1575704965 }
];

db.insertMany(users);
```

OR

`db.collection.insertMany([{name: 'Mohammad MohammadAlian', ip: '127.0.0.1', lastLoginTime: 1575704736}, {name: 'John Doe', ip: '10.10.10.10', lastLoginTime: 1575704965}])`;

# Querying

## find

retrieve all of documents

`db.collection.find()` OR `db.collection.find({})`

query by value of specific field

`db.collection.find({name: 'Mohammad MohammadAlian'})`

querying throw nested field

```javascript
var user = { name: "John", job: { title: "programmer", salary: 125000 } };
```

if we want to find above user by job title we could use following command

`db.collection.find({'job.title': 'programmer'})`

using regex

`db.collection.find({name: /M.*/})`

## pretty

make results pretty 😁

`db.collection.find().pretty()`

## limit

`db.collection.find().limit(10)`

NOTE: 10 is count of documents which will be retrieved

## skip

skip result

`db.collection.find().skip(2)`

NOTE: 2 is count of documents which will be skipped

## sort

show sorted result

`db.collection.find().sort({fieldName: 1})`

NOTE: 1 is ascending and -1 is descending

## count

retrieve count of results

`db.collection.find().count()`

## distinct

retrieve distinct value

`db.collection.distinct('name')`

NOTE: name is a field

for nested field we can use following command

`db.collection.distinct('comments.message')`

## Operators

### less than

`db.collection.find({field: {$lt: 200}})`

### less than or equal

`db.collection.find({field: {$lte: 200}})`

### greater than

`db.collection.find({field: {$gt: 200}})`

### greater than or equal

`db.collection.find({field: {$gte: 200}})`

### not equal

`db.collection.find({field: {$ne: 'string is also accepted in some operators'}})`

### in

`db.collection.find({field: {$in: [1999,2010,2019,2022]}})`

### all

`db.collection.find({field: {$all: [1999,2010]}})`

### slice

`db.collection.find({arrayField: {$slice: 3}})`

### or

`db.collection.find({$or: [{filed: 'value'}, {field: 'value'}]})`

### mod

modulo operator
`db.collection.find({field: {$mod: [100,0]}})`

### size

`db.collection.find({arrayFiled: {$size: 2}})`

### exists

`db.collection.find({field: {$exists: true}})`

### type

[type numbers](https://docs.mongodb.com/manual/reference/bson-types/)
`db.collection.find({field: {$type: 2}})`

## Update document

general form

`db.collection.update({query}, {update}, {flags})`

example

`db.collection.update({field: 'value'}, {$set: {otherField: 'new Value'}}, {upsert: true})`

### inc

increment value

`db.collection.updateOne({field: 'value'}, {$inc: {number: 6}})`

Increases six units of number

### unset

`db.collection.updateOne({field: 'value'}, {$unset: {anotherField: 1}})`

this will be remove anotherField where field equal value

### push

push value to array

`db.collection.updateOne({_id: 1}, {$push: {numbers: 6}})`

push six into numbers where id is 1

### each

`db.collection.updateOne({_id: 1}, {$push:{numbersArray: {$each: ['R','T', 'H']}}})`

add each value to numbersArray where id is 1

### addToSet

push to array if not exists

`db.collection.updateOne({_id:1}, {$addToSet: {numbers: 565}})`

### pop

`db.collection.updateOne({_id: 1}, {$pop: {numbers: -1}})`
1: from end
-1: from beginning

### pull

`db.collection.updateOne({_id: 1}, {$pull: {numbers: 5}})`

remove all 5 in numbers Array where id is 1
