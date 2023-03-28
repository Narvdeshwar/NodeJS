# What is Nodejs
1. Nodejs is not a language it is server enviroment.
2. Nodejs can connect with database.
3. code and syntax is similiar to JavaScript but not same.
4. NodeJS free, Open-source and it uses **Chrome VM8** engine to execute code.

# Basic Nodejs Server
```js
//importing http module
const http=require('http') 
//this module handle http req and res

http.createServer((req,res)=>{
    res.write("<h1>Hello world</h1>");
    res.end();
}).listen(4000)
//createServer()=> this function takes funtion as a parameter
```
# passing fuction as parameter
```js
```
# Making static api

# JSON.stringyfy()
