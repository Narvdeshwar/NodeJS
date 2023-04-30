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
### homepage
![Screenshot from 2023-04-07 09-30-57](https://user-images.githubusercontent.com/56790381/230538546-2d9e65d3-07b3-404b-8d94-2039050fb75a.png)
### about page
![Screenshot from 2023-04-07 09-31-09](https://user-images.githubusercontent.com/56790381/230538555-3a33305f-3fdf-4775-aeda-6d3be504fdf6.png)

## removing extension 
```js
const express = require('express');
const path=require('path');

const port=4500
const app=express(); //executable express 

const publicPath=path.join(__dirname,'public');

app.get('/',(req,res)=>{
    res.sendFile(`${publicPath}/index.html`);    
})

app.get('/about',(req,res)=>{
    res.sendFile(`${publicPath}/about.html`)
})
// execute below code if above file path doesn't exits
app.get('*',(req,res)=>{
    res.sendFile(`${publicPath}/404.html`)
})
app.listen(port,()=>{
    console.log(`app is running at port ${port}`);
})
```
### homepage
![Screenshot from 2023-04-07 19-44-18](https://user-images.githubusercontent.com/56790381/230624782-9b0ce94f-54e8-441c-9e08-d337345bca54.png)
### about page
![Screenshot from 2023-04-07 19-44-35](https://user-images.githubusercontent.com/56790381/230624791-0cc9a8e9-719b-431a-a023-8f3049b3253b.png)
### 404 page
![Screenshot from 2023-04-07 19-44-45](https://user-images.githubusercontent.com/56790381/230624794-3ebe2d73-1c0c-47c1-8da5-427d0755bd28.png)

# middleware 
middleware are the function which are used with routes and also helps to access reqeuest and response and also modify them.
```js
const express=require('express');
const app=express();
const reqFilter=(req,res,next)=>{
    if(req.query.age<18){ // if requested age will be below this 
        res.send("you can't access this page");
    } // others wise access this
    else{
        next();
    }
}
app.use(reqFilter);
app.get('/',(req,res)=>{
    res.send('hello');
})
app.listen(4000,()=>{
    console.log('app is running');
})
```
## if requested query age is below 18
![Screenshot from 2023-04-30 10-48-59](https://user-images.githubusercontent.com/56790381/235337072-ca09bd81-d2ad-4777-b8f5-2d9e4fda3ee8.png)
## if requested query age is greater than 18
![Screenshot from 2023-04-30 10-49-18](https://user-images.githubusercontent.com/56790381/235337069-2b0fbf0f-a0be-45bd-a8bd-632ba773b386.png)

