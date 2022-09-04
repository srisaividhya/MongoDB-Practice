Query / Find Documents
query the movies collection to

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

Update Documents
1. add a synopsis to "The Hobbit: An Unexpected Journey" : "A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug."
db.movies.update({title:'The Hobbit: An Unexpected Journey'}, {$set:{synopsis:'A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug.'}})

2. add a synopsis to "The Hobbit: The Desolation of Smaug" : "The dwarves, along with Bilbo Baggins and Gandalf the Grey, continue their quest to reclaim Erebor, their homeland, from Smaug. Bilbo Baggins is in possession of a mysterious and magical ring."
db.movies.update({title:'The Hobbit: The Desolation of Smaug'}, {$set:{synopsis:'The dwarves, along with Bilbo Baggins and Gandalf the Grey, continue their quest to reclaim Erebor, their homeland, from Smaug. Bilbo Baggins is in possession of a mysterious and magical ring.'}})

3. add an actor named "Samuel L. Jackson" to the movie "Pulp Fiction"
 db.movies.updateOne({title: 'Pulp Fiction'}, {$push:{actors:'Samuel L. Jackson'}})
 
 Text Search
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

Delete Documents
1. delete the movie "Pee Wee Herman's Big Adventure"
db.movies.deleteOne({title:'Pee Wee Hermans Big Adventure'})

2. delete the movie "Avatar"
db.movies.deleteOne({title:'Avatar'})

Relationships

Insert the following documents into a users collection 
username : GoodGuyGreg first_name : "Good Guy" last_name : "Greg" 
db.users.insertOne({username:"GoodGuyGreg",first_name:"Good Guy",last_name:"Greg"})
     
username : ScumbagSteve full_name : first : "Scumbag" last : "Steve"
db.users.insertOne({username":"ScumbagSteve","full_name":{"first":"Scumbag","last":"Steve"}})


Insert the following documents into a posts collection 

username : GoodGuyGreg title : Passes out at party body : Wakes up early and cleans house
db.posts.insertOne({ username: "GoodGuyGreg", title: 'Passes out at party', body: "Waks up early and cleans house" })

username : GoodGuyGreg title : Steals your identity body : Raises your credit score 
    db.posts.insertOne({
... username: "GoodGuyGreg",title :'Steals your identity', body: "Raises your credit score"})

username : GoodGuyGreg title : Reports a bug in your code body : Sends you a Pull Request
db.posts.insertOne({ username: "GoodGuyGreg", title: 'Reports a bug in your code', body: "Sends you a Pull Request" })


 username : ScumbagSteve title : Borrows something body : Sells it 
db.posts.insertOne({ username: "ScumbagSteve", title: 'Borrows something', body: "Sells it" })

username : ScumbagSteve title : Borrows everything body : The end 
db.posts.insertOne({ username: "ScumbagSteve", title: 'borrows everything', body: "The end" })

username : ScumbagSteve title : Forks your repo on github body : Sets to private
db.posts.insertOne({ username: "ScumbagSteve", title: 'Forks your repo on github', body: "Sets to private" })


Insert the following documents into a comments collection

username : GoodGuyGreg comment : Hope you got a good deal! post : [post_obj_id]
where [post_obj_id] is the ObjectId of the posts document: "Borrows something"
db.comments.insertOne({ username: "GoodGuyGreg", comment: "Hope you got a good deal!", post: ObjectId("6314c168056b571fd1160cd3") })


username : GoodGuyGreg comment : What's mine is yours! post : [post_obj_id]
where [post_obj_id] is the ObjectId of the posts document: "Borrows everything"
db.comments.insertOne({ username: "GoodGuyGreg", comment: "What's mine is yours!", post: ObjectId("6314c19a056b571fd1160cd4") })


username : GoodGuyGreg comment : Don't violate the licensing agreement! post : [post_obj_id]
where [post_obj_id] is the ObjectId of the posts document: "Forks your repo on github
db.comments.insertOne({ username: "GoodGuyGreg", comment: "Don't violate the licensing agreement", post: ObjectId("6314c1bc056b571fd1160cd5") })


username : ScumbagSteve comment : It still isn't clean post : [post_obj_id]
where [post_obj_id] is the ObjectId of the posts document: "Passes out at party"

db.comments.insertOne({ username: "ScumbagSteve", comment: "It still isn't clean", post:ObjectId("6314c10f056b571fd1160cd1") })



username : ScumbagSteve comment : Denied your PR cause I found a hack post : [post_obj_id]
where [post_obj_id] is the ObjectId of the posts document: "Reports a bug in your code"
db.comments.insertOne({ username: "ScumbagSteve", comment: "Denied your PR cause i found a hack", post:ObjectId("6314c13a056b571fd1160cd2") })

Querying related collections
1. find all users
db.users.find().pretty()

2. find all posts
 db.posts.find().pretty()

3. find all posts that was authored by "GoodGuyGreg"
db.posts.find({username: "GoodGuyGreg"})

4. find all posts that was authored by "ScumbagSteve"
db.posts.find({username: "ScumbagSteve"})

5. find all comments
db.comments.find().pretty()

6. find all comments that was authored by "GoodGuyGreg"
db.comments.find({ username: "GoodGuyGreg"})

7. find all comments that was authored by "ScumbagSteve"
db.comments.find({ username: "ScumbagSteve"})

8. find all comments belonging to the post "Reports a bug in your code"

