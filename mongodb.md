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
