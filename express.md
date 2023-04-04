# Express 
It is framework of Nodejs.
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
# output 
[
![Screenshot from 2023-04-04 21-58-04](https://user-images.githubusercontent.com/56790381/229857542-abe0d40d-40e0-4f3a-b630-692a6b8f9ee4.png)]
