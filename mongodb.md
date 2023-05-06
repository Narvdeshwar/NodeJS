# Mongodb
1. Mongodb is a no-sql database.
2. The data stored in the form of collection not in the form of a table as in SQL.
3. Collections don’t have rows and columns.
4. Data is stored in the form of objects.
## connecting mongdb with database
```js
const {MongoClient} = require('mongodb');
const url='mongodb+srv://Eternal:<password>@testdb.l9j5njr.mongodb.net/?retryWrites=true&w=majority'; //connecting with cloud database
const client=new MongoClient(url);
async function getData(){
    const result=await client.connect();
    const db=result.db('e-com');
    const collection=db.collection('products')
    console.log(await collection.find().toArray());
}
getData();

```
### output

![Screenshot from 2023-05-05 14-21-08](https://user-images.githubusercontent.com/56790381/236415802-1e2ec06f-c497-454c-b396-9747ea18a986.png)
### accesing data/reading data
```js
//dbConnect.js database connection seprate file
const {MongoClient} = require('mongodb');
const url='mongodb+srv://Eternal:AshrithXYZ@testdb.l9j5njr.mongodb.net/?retryWrites=true&w=majority';
const client=new MongoClient(url);
dbConnect=async()=>{
    const result=await client.connect();
    const db=result.db('e-com');
    return db.collection('products');
}
module.exports=dbConnect;
```

```js
//Accesing data from two different ways by handling the promise
const dbConnect = require('./dbConnect');
dbConnect().then((res)=>{
    res.find().toArray().then((data)=>{
        console.log(data);
    })
})
const data=async ()=>{
    let result=await dbConnect();
    result=await  result.find().toArray()
    console.log(result);
}
data();
```
### insert data in database
```js
const dbConnect = require('./dbConnect');
const insertData=async()=>{
    const db=await dbConnect();
    const result=await db.insertMany(
        {"name":"redmi note 5 pro","brand":"xiomi","price":11999}
    )
    if(result.acknowledged){
        console.log("data inserted succuessfully");
    }
    else{
        console.log("Some error occured");
    }
}
insertData();
/**
 * You can add multiple entry by using array.
 * const result=await db.insertOne(
        [
            {"name":"redmi note 7 pro","brand":"xiomi","price":14999},
            {"name":"redmi note 6 pro","brand":"xiomi","price":12999}

        ]
    )
 */
```
### update data in database
```js
const dbConnect = require('./dbConnect');
const updateData = async () => {
    const db = await dbConnect();
    const result = await db.updateOne(
        { "name": "redmi note 9 pro" },
        { $set: { "name": "note 9 pro" } }
    )
    if(result.modifiedCount==1){
        console.log("data updated succuessfully");
    }
    else{
        console.log("oops! data not updated");
    }
}
updateData();
```
### delete data in database
```js
const dbConnect=require('./dbConnect');
const deleteData=async()=>{
    const db=await dbConnect();
    const result=await db.deleteOne(
        {"name":"note 9 pro"}
    )
    if(result.deletedCount>0){
        console.log("data deleted succussfully");
    }
    else{
        console.log("no more data exits to delete.");
    }
}
deleteData()
```
## Basic crud api
```js
 const express = require('express');
const mongoDB = require('mongodb');
const dbConnect = require('./dbConnect');
const app = express();

/**
 * For fetching the data we use GET method
 */
app.get('/', async (req, res) => {
    const db = await dbConnect();
    const result = await db.find().toArray();
    res.send(result)
})

/**
 * For inserting data we use POST method
 */
app.use(express.json());
app.post('/insert', async (req, res) => {
    const db = await dbConnect();
    const result = await db.insertOne(req.body)
    if(result.acknowledged){
        res.send("data inserted successfully");
    }
    else{
        res.send("oops! some error occured");
    }
})
/**
 * For updating data we use PUT method
 */
app.put('/update',async (req,res)=>{
    const db=await dbConnect();
    const result=await db.updateOne(
        {"name":"vivo v50"},
        {$set: req.body}
    )
    if(result.modifiedCount==1){
        res.send("data updated successfully");
    }
    else{
        res.send("data already updated !");
    }
})
/**
 * For deleting data we DELETE method
 */

app.delete('/delete/:id',async(req,res)=>{
    const db=await dbConnect();
    const result=await db.deleteOne(
        {_id:new mongoDB.ObjectId(req.params.id)}
    )
    if(result.deletedCount>0){
        res.send("data deleted successfully");
    }
    else{
        res.send("some error occured");
    }
})

app.listen(4000, () => {
    console.log("server is running !");
})
```
