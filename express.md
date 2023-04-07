# Express 
It is framework of Nodejs.

# basic server
```js
const express = require('express');
const port=4500
const app=express(); //executable express 

// default page
app.get('',(req,res)=>{
    res.send("This is home page")
})

// about apge 
app.get('/about',(req,res)=>{
    res.send('this is about page');
})

app.listen(port,()=>{
    console.log(`app is running at port ${port}`);
})
```
## output for homepage
![Screenshot from 2023-04-04 21-58-04](https://user-images.githubusercontent.com/56790381/229857542-abe0d40d-40e0-4f3a-b630-692a6b8f9ee4.png)
## output for about page
![Screenshot from 2023-04-04 22-04-03](https://user-images.githubusercontent.com/56790381/229858288-0eb2310c-62ac-4d50-84e8-2cf1b27f2ac5.png)

# runing static html page
```js
const express = require('express');
const path=require('path');

const port=4500
const app=express(); //executable express 

const publicPath=path.join(__dirname,'public','/');

app.use(express.static(publicPath));
// app.use() is a middleware
// express.static() load static content from its given argument

app.listen(port,()=>{
    console.log(`app is running at port ${port}`);
})
```


