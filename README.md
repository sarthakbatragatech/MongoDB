# Mongo DB Notes

## Introduction

- Learnt what MongoDB is and can do

- Atlas, MongoDB as a service

- Installed Compass, connected to MongoDB

- Databases, Collections, and Documents

- Databases contain collections

- Access by: database.collection

- Schema, datatypes, Scalar value types and ranges for a field

- Nested fields

- Documents in fields, arrays in fields

- Filter queuries and JSON Documents

- Fields, having two parts: key (string) and value

- {'end station name': 'Broadway'}

- {'birth year': {$gte: 1985,$lt: 1990}}

- {coordinates: {$geoWithin: { $centerSphere: [ [ -66.46872628141023, 18.15077441048423 ], 0.015283221050021297 ]}}}

- JSON Documents support any level of heirarchy that is appropriate to your application's data model

- MongoDB's query language, indexes, and internal data structures are designed to support a wide variety of data models

## The MongoDB Query Language + Atlas

- Create, Read, Update, and Delete (CRUD) operations

- Used the Mongo shell which provides full support for the query language

- Installed MongoDB as a service (Enterprise)

- Connected to a cluster

- Give it a list of all servers on the cluster

- Replica sets

- Only primary's can accept writes, there is only one primary for a cluster

- Created a cluster on AWS

- Sanbox cluster will allow writes

- Connected to my own sandbox atlas cluster it from shell

- Connected to sandbox from compass

- Created collection and documents from shell and compass

- insert1 ( db.moviesScratch.insertOne({title: "Star Trek II: The Wrath of Khan", year: 1982, imdb: "tt0084726"}) ) to add a document to sandbox from shell

- insertmany (Lot of noise in the data or errors, might result in exceptions)

- Use unordered

- Search for array element at index 1 (second position) {"genres.1": "Western"}

- Cursors

- it, short for iterate, gives the next 20 results in the set.

- Projections

- Include titles db.movieDetails.find({"genres": ["Family"]}, {title: 1})

- db.movieDetails.find({"genres": ["Family"]}, {title: 1, _id: 0})

- In RDB, all records must have same set of columns

- In MongoDB, we don't include the field for a record where we don't have the data

- To update, $set. All key values in the update document are reflected in the new version of the document we are updating. If there were an existing field, it would overwrite it.

- Other updateOne operators: $unset, $min, $inc, $push, $each

- upsert: True, Update documents matching the filter, if there are none, insert the update document as a new document in the collection

- Used to make sure we don't enter duplicate values

- replaceOne:

## Query Operators

- Deeper Dive on the MongoDB Query Language Query operators: element operators, logical operators, array operators, and the regex operator

- Query operators: https://docs.mongodb.com/manual/reference/operator/query/

- db.movieDetails.find({runtime: {$gte: 90, $lte: 120}}, {_id: 0, title: 1, runtime: 1}).count()

- $ne: not equal to

- $in: in the array

- {rated: {$in: ["PG", "R"]}}

- $exist, $type

- Logical Operators: $or, $and, $not, $nor

- Takes in an array as an argument

- Any one of the values in the array apply to the argument

- $and used for situations where we need to specify multiple criteria on the same field

- db.shipwrecks.find({$and: [{watlev: "always dry"}, {depth: 0}]}).count()

-$all

- db.movieDetails.find({genres: {$all: ["Comedy", "Crime", "Drama"]}}, {_id: 0, title: 1, genres: 1}).pretty()

-$elemMatch

- db.movieDetails.find({boxOffice: {$elemMatch: {"country": "Germany", "revenue": {$gt: 17}}}}).count()

- Match fields in a array in a document based on a criteria
