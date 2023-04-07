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
function sum(a,b){
    return a+b;
}
function ans(sum){
    const res=sum(2,3)
    console.log(res); // 5
}
ans(sum)

```
# Making simple API
```js
const http=require('http');

const data={'name':'Ashrith','branch':'CSE','rollno':'1904220109009'};

const app=http.createServer((req,res)=>{
    res.writeHead(200,{'Content-Type':'application/json'}) 
    res.write(JSON.stringify(data))
    res.end()
})

app.listen(4500,()=>{
    console.log('app is running');
})
```
## res.writeHead(): 
1. it is inbuild property of http module which sends a response header to request.
2.  **Syntax:** res.writeHead(statusCode,statusMessage,header)

# JSON.stringify()
