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

```bash
var user = {name: 'Mohammad MohammadAlian', ip: '127.0.0.1', lastLoginTime: 1575704736};

db.insertOne(user)
```

OR

`db.collection.insertOne({name: 'Mohammad MohammadAlian', ip: '127.0.0.1', lastLoginTime: 1575704736})`;

to insert many object in one query you can use insertMany function

```bash
var users = [{name: 'Mohammad MohammadAlian', ip: '127.0.0.1', lastLoginTime: 1575704736}, {name: 'John Doe', ip: '10.10.10.10', lastLoginTime: 1575704965}];

db.insertMany(users)
```

OR

`db.collection.insertMany([{name: 'Mohammad MohammadAlian', ip: '127.0.0.1', lastLoginTime: 1575704736}, {name: 'John Doe', ip: '10.10.10.10', lastLoginTime: 1575704965}])`;

# Querying

query by value of specific field value

`db.collection.find({name: 'Mohammad MohammadAlian'})`

querying throw nested field

```
var user = {name: 'John', job: {title: 'programmer', salary: 125000}};
```

if we want to find above user by job title we could use following command

`db.collection.find({'job.title': 'programmer'})`
