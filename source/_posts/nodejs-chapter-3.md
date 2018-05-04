---
title: nodejs-chapter-3
date: 2018-05-02
tags: [nodejs]
categories: 童长钱
description: nodejs file system（文件系统）
---

### File System？  
**File System** 是Node中使用最为频繁的模块之一，该模块提供了读写文件系统的能力。 
浏览器中的JavaScript没有读写本地文件系统的能力(忽略IE中的ActiveX),而Node作服务器编程语言，伟岸系统API是必须的，File System模块包含了数十个文件操作的API，[查阅API](https://nodejs.org/dist/latest-v8.x/docs/api//fs.html)
<!--more-->
#### 下面介绍几个常用的API
1. **readFile**

声明如下：    
``` node.js
fs.readFile(file[,options,callback])#  
Added: v0.1.29  
file <String> | <Buffer> | <Integer> filename of file descriptor  
options <Object> | <String>  
encoding <String> | <Null> default  = null  
flag <String> defult = "r"  
callblack = <Function>
```  
readFile 方法用异步来读取文件中的内容，例如：  

``` node.js
var fs= require("fs");
var data = fs.readFileSync("foo.txt",function (err,data){
    if (err) thorw err;
    console.log(data);
});
``` 
*readFile*会将一个文件的全部内容读到内存中，适用于提交较小的文本；如果有一个数百MB大小的文件需要读取，建议不要使用readFile而是选择stream。readFile读出的数据需要在回调方法中获取，而readFileSync直接返回文本数据内容。  

``` node.js
var fs= require("fs");
var data = fs.readFileSync("foo.txt",{encoding:"UTF-8"});
console.log(data);
```   

如果不指定File的encoding配置，readFile会直接返回类似Buffer格式；如果希望得到的是字符串形式，还需要调用toString方法进行转化.

2. **writeFile**  

声明如下：  

``` node.js
fs.writeFile(file, data[, option],callback);
file <String> | <Buffer> | <Integer> filename of file descriptor  
data <String> | <Bufer>
options <Object> | <String>  
encoding <String> | <Null> default  = null  
mode <Integer> defult = 0o666  
flag <String> defult = "w"  
callblack = <Function>
```   
在WriteFile的第一个参数文件名，如果不存在，则会尝试创建它(默认flag为w)。  

``` node.js
var fs = require("fs");
fs.writeFile("foo.txt", "你好", { flag: "a", encoding: "UTF-8" }, function (err) {
    if (err) {
        console.log(err);
        return;
    }
    console.log("success");
});
```  
3. **fs.stat(path,callback)**  
stat方法通常用来获取3文件状态。  
通常开发者可以再调用opne(),read(),或者write方法之前调用fs.stat方法，用来判断文件是否存在。  
    
``` node.js
var fs = require("fs");
fs.stat("test.txt",function(err,result){
    if (err){
        console.log(err);
        return;
    }
    console.log(result);
});
```   

文件存在返回文件信息，如果不存在则会出现Error ENOENT：no such file or director的错误。  

4. **fs.stat和fs.fstat的区别**

声明如下：  

``` node.js
fs.fstat(fd,callback)
```  

fs.stat和fs.fstat在功能上是等价的，唯一的区别是fstat第一个参数是文件的描述符，格式为Integer，因此fstat方法通常搭配open方法使用，因为open方法返回得到结果就是一个文件描述。  
 
``` node.js
var fs = require("fs");
fs.open("test.txt","a",function (err,fd){
    if (err){
        console.log();
        return;
    }
    console.log(fd);
    fs.fstat(fd,function(err,result){
        if (err){
            console.log(err);
            return;
        }
        console.log(result);
    });
});
```   

下面是一个例子————获取目录下所有的文件名，这是一个常见的需求，实现这个功能只需要fs.readFile以及fs.stat连个API，readdir用于获取目录下所有的问文件或者子目录，stat用来判断具体每条记录是文件还是子目录，如果是子目录，则递归调用整个方法。  

``` node.js
var fs = require("fs");
function getAllFileFromPath(path) {
    fs.readdir(path, function (err, res) {
        for (var subPath of res) {
            //这里使用同步方法而非异步
            var statObj = fs.statSync(path + "/" + subPath);
            if (statObj.isDirectory()) {//判断是否为目录
                console.log("Dir:", subPath);
                getAllFileFromPath(path + "/" + subPath)
            } else {
                console.log("File:", subPath);
            }
        }
    })
}
getAllFileFromPath(__dirname);
``` 