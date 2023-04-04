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
