# Mongo 101

- No Schema
- Doucment based
- Sclable

# BSON

- Current max size 16 MB.
- PK auto-inserted (`ObjectId`)

https://docs.mongodb.com/manual/mongo/ [Ref Manual]

# commands

| Description            | Commands                              | comments                    |
| ---------------------- | ------------------------------------- | --------------------------- |
| Start Server           | `mongod`                              |
| Start Client           | `mongo`                               |
| UI                     | Compass                               |                             |
| Show DataBases         | `show dbs`                            |
| Create or Switch to DB | `use db-name`                         |
| Create Collection      | `db.db-name.insertOne({key:"value"})` | quotes on keys are optional |
| Insert 1 Document      | `db.db-name.insertOne({key:"value"`   |                             |
| Insert Many Documents  | `db.db-name.insertMany([{},{},...]})` | array of objects            |
| Show all documents     | `db.db-name.find()`                   |                             |

# Query

| Description                                                               | Commands                                                            | comments                                                                                                                                                                                        |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Query All Documents                                                       | `db.db-name.find()`                                                 |                                                                                                                                                                                                 |
| Search by Filter                                                          | `db.db-name.find({key:"value"`})                                    | ex: `db.db-name.find({name:"test user"`})                                                                                                                                                       |
| Mongo Operator                                                            | `$`                                                                 | `{price:{$lte:500}}`                                                                                                                                                                            |
| Comparision Operators                                                     |                                                                     | `$lt` => Less Than `$lte` => Less Than or qual , `$gte, $gt`                                                                                                                                    |
| Multiple Criteria `AND`                                                   | `db.db-name.find({price:{$lt:500}, rating:{$gte:4.8}}`              | find document which have price less than `500` `AND` rating greater than `4.8`                                                                                                                  |
| Multiple Criteria `OR`                                                    | `db.db-name.find({$or: [ {price:{$lte:500}}, {rating:{$gte:4.8}}]}` | find document which have price less than `500` `OR` rating greater than `4.8`                                                                                                                   |
| Projection: rather than whole `Obj` return return fields that are queried | `db.db-name.find({prince:{$lte:4000}}, {name:1})`                   | outputs `ObjectId, Name`                                                                                                                                                                        |
| Update Document                                                           | `db.db-name.updateOne({name:"test User"},{ $set: {salary:4000} })`  | find user `test user` update salary to `4000` this will update single document `updateOne` use `updateMany` to update more than One document. \*update will create a new KV pair if didnt found |
| Update Whole Doc `Replace`                                                | `db.db-name.replaceOne({...,...,...})`                              | `replaceOne(), replaceMany()`                                                                                                                                                                   |
| Delete Document                                                           | `db.db-name.deleteOne({name:"Test"})`                               | `deleteOne, deleteMany`                                                                                                                                                                         |
| Delete Everything                                                         | `db.db-name.deleteMany({})`                                         | \*careful                                                                                                                                                                                       |


### Mongooese
- object data modeling (ODM)

connection:`mongoose.connect(DATABASE,{options}).then(con => consol.log("DB connected")`

Model: Blueprint to create documents

1.Create a Schema

2.Create Model form that Schema

3.Create Document from Model

1. Create Schema
```
const tours = mongooese.Schema({
 name: {
    //Schema type options
    type: String,
    required: [true, 'A tour must have a name'], //Validator:  Errors if false
    unique: true
  },
  rating: {
    type: Number,
    default: 4.5 // Default value
  },
  price: Number
});
```
2. Create Model
```
const Tour = mongooes.Model('Tour', tourSchema);
```
3. Document Model
```
const testTour = new Tour({
name:"A test Tour",
price:3000
});
```
3.1 Saving Data to DB
```
testTour.save()
.then(doc => {console.log(doc)}) // resolved value returns final document.
.catch(err => console.log('error');
```


