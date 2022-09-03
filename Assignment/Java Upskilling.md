1. get all documents
db.movies.find().pretty()

2. get all documents with writer set to "Quentin Tarantino"
 db.movies.find({writer: 'Quentin Tarantino'})

3. get all documents where actors include "Brad Pitt"
db.movies.find({actors:'Brad Pitt'})

4. get all documents with franchise set to "The Hobbit"
 db.movies.find({franchise: 'The Hobbit'})


5. get all movies released in the 90s
db.movies.find({year: {$gte: 1990 , $lt : 2000}})

6. get all movies released before the year 2000 or after 2010
db.movies.find({$or:[{year:{$gt:2010}},{year:{$lt:2000}}]})


1. find all movies that have a synopsis that contains the word "Bilbo"
db.movies.find({synopsis: {$regex: 'Bilbo'}})

2. find all movies that have a synopsis that contains the word "Gandalf"
db.movies.find({synopsis: {$regex: 'Gandalf'}})

3. find all movies that have a synopsis that contains the word "Bilbo" and not the word "Gandalf"
 db.movies.find({$and:[{synopsis:{$regex: 'Bilbo'}},{synopsis:{$not: /Gandalf/}}]})

4. find all movies that have a synopsis that contains the word "dwarves" or "hobbit"
db.movies.find({$or:[{synopsis:{$regex: 'dwarves'}},{synopsis:{$regex:'hobbit'}}]})

5. find all movies that have a synopsis that contains the word "gold" and "dragon"
db.movies.find({$and:[{synopsis:{$regex: 'gold'}},{synopsis:{$regex:'dragon'}}]})

