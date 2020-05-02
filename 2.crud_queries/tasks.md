1. Create a database named `blog`.
```
use blog
```

2. Create a collection called 'articles'.
```
db.createCollection('articles');
```

3. Insert multiple documents(at least 3) into articles. It should have fields
```
class Article {
  constructor(title, author, tags, details) {
    this.title = title;
    this.author = author;
    this.tags = tags;
    this.details = details;
  }
}

class Author {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const author1 = new Author('Reettik', 22);
const author2 = new Author('Kabir', 28);
const article1 = new Article('Article 1', author1, ['html'], 'This article is about HTML');
const article2 = new Article('Article 2', author2, ['javascript', 'jquery'], 'This article is about jQuery');
const article3 = new Article('Article 3', author1, ['node'], 'This article is about Node');

db.articles.insertMany([article1, article2, article3]);
```

4. Find all the articles using `db.COLLECTION_NAME.find()`
```
db.articles.find({});
```

5. Find a document using _id field.
```
db.articles.find({_id: ObjectId('5ea9a99d7197b5e7fdc701a6')});
```
6. Find documents using title and author's name field.
```
db.articles.find({title: 'Article 1', 'author.name': 'Reettik'});
```
7. Find document using a specific tag.
```
db.articles.find({tags: 'jquery'});
```

8. Update title of a document using its _id field.
```
db.articles.update({_id: ObjectId('5ea9a99d7197b5e7fdc701a6')}, {$set : {title: 'Article 1 updated'}});
```

9.  Update a author's name using article's title.
```
db.articles.update({title: 'Article 2'}, {$set : {'author.name': 'Kabir Singh'}});
```

10. rename details field to description from articles collection. 
```
db.articles.updateMany({}, {$rename: {'details': 'description'}});
```

11. Add additional tag in a specific document.
```
db.articles.update({title: 'Article 3'}, {$push: {tags: 'backend'}});
```

12. Update an article's tags using $set and without $set.
```
db.articles.update({title: 'Article 3'}, {$set: {tags: ['one', 'two']}});
```
  - Write the differences here ?

13. Increment an auhtor's age by 5.
```
db.articles.updateMany({'author.name': 'Reettik'}, {$inc: {'author.age': 5}});
```  

14. Delete a document using _id field with `db.COLLECTION_NAME.remove()`.
```
db.articles.remove({_id: ObjectId('5ea9abbe7197b5e7fdc701ab')});
```

Use sample.js data for below queries.

1. Find all males who play cricket.
```
db.users.find({sports: 'cricket'});
```

2. Update user with extra golf field in sports array whose name is "Steve Ortega".
```
db.users.updateOne({name: 'Steve Ortega'}, {$push: {sports: 'golf'}});
```

3. Find all users who play either 'football' or 'cricket'.
```
db.users.find({$or : [{sports: 'football'}, {sports: 'cricket'}]});
```

4. Find all users whose name includes 'ri' in their name.
```
db.users.find({name: /ri/});
```
