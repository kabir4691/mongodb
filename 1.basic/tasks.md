#### write commands for following mongodb opertaions

1. create a database named `sports`
```
use sports
```

1. list all databases present in local mongod server.
```
show dbs
```

3. create 3 collections named `cricket`, `football`, `TT` in sports database.
```
use dbs
db.createCollection('cricket');
db.createCollection('football');
db.createCollection('TT');
```

4. add 3 players in each of above collections which should have fields like `name`, `age`, `email`, state and auction_price.
```
class Player { 
  constructor(name, age, email, state, auctionPrice) {
    this.name = name;
    this.age = age;
    this.email = email;
    this.state = state;
    this.auction_price = auctionPrice;
  }
}
const player1 = new Player('Kabir', 28, 'kabir@altcampus.com', 'Tamil Nadu', -1);
const player2 = new Player('Reettik', 22, 'reettik@altcampus.com', 'West Bengal', 5);
const player3 = new Player('Tejas', 24, 'tejas@altcampus.com', 'Karnataka', 100);
const players = [player1, player2, player3];
db.getCollectionNames().forEach(collection => {
  db[collection].insertMany(players);
});
```

1. list all collections in sports database.
```
show collections
```

1. rename `TT` collection to `tennis`.
```
db.TT.renameCollection('tennis');
```

3. create a capped collection called `khokho` which should have max 3 documents.
  Try inserting more than 3 and output the result here ?
```
db.createCollection('khokho', { capped: true, size: 512, max: 3});
> db.khokho.insert({});
WriteResult({ "nInserted" : 1 })
> db.khokho.insert({});
WriteResult({ "nInserted" : 1 })
> db.khokho.insert({});
WriteResult({ "nInserted" : 1 })
> db.khokho.find()
{ "_id" : ObjectId("5ea6c4d77f545e84724a649c") }
{ "_id" : ObjectId("5ea6c4d87f545e84724a649d") }
{ "_id" : ObjectId("5ea6c4da7f545e84724a649e") }
> db.khokho.insert({});
WriteResult({ "nInserted" : 1 })
> db.khokho.find()
{ "_id" : ObjectId("5ea6c4d87f545e84724a649d") }
{ "_id" : ObjectId("5ea6c4da7f545e84724a649e") }
{ "_id" : ObjectId("5ea6c4e87f545e84724a649f") }
```

1. check whether a collection is capped or not?
```
db.khokho.isCapped()
```

2. remove all documents from `football` collection.
```
// For uncapped collection
db.football.remove({})
// For capped collection
db.khokho.drop()
db.createCollection('khokho', { capped: true, size: 512, max: 3});
```

1.  delete cricket collection completely.
```
db.cricket.drop()
```

2.  rename database sports to games
```
// Method 1
use sports
db.getCollectionNames().forEach(collection => {
    db[collection].find().forEach(document => {
        db.getSiblingDB('games')[collection].insert(document); 
    }) 
});
db.dropDatabase();

// Method 2
// In normal terminal
mongodump --archive="mongodump-sports-db" --db=sports
mongorestore --archive="mongodump-sports-db" --nsFrom='sports.*' --nsFrom='games.*'
// In mongo shell
use sports
db.dropDatabase();
```

1.  delete sports database. 
```
use sports
```