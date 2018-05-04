---
title: nodejs-chapter-2
date: 2018-05-02
tags: [nodejs]
categories: 童长钱
description: nodejs Buffer的相关知识
---

### Buffer？  

**Buffer**是Node特有的一种数据类型，主要用来处理二进制数据。  

**Buffer**属于固有（built）类型无需使用require引入。  

例如下面例子：    
``` node.js
var fs = require("fs");
fs.readFile("foo.text",function (err,results){
    console.log(results);
});
//结果：<Buffer 48 65 6c 6f 20 57 6f 72 6c 64 >(hellow node)  
```    
上面的代码中，最后打印出的是十六进制的数据，由于纯二进制格式太长而且难以阅读，Buffer通常表现为十六进制的字符串。  

<!--more-->
### Buffer的构建以转换  

buffer类初始化一个buffer对象，参数可以是二进制数据组成的数组：    
``` node.js
var buffer = Buffer([0x48,0x65,0x6c,0x6c,0x6c,0x6f,0x20,0x4e,0x64f,0x64,0x65]);  
//结果：hellow node  
```  
如果想有一个字符串来得到一个Buffer，同样可以实现，例如：  
``` node.js
var buffer = new Buffer("Hellow Node");
console.log(buffer);
//结果：<Buffer 48 65 6c 6f 20 4e 6f 64 65>
```  
**注意**：在最新的Node API中，Buffer()方法被标记为Depecated(“不赞同”的意思)，表示不推荐使用;目前推荐使用Buffer.from方法来初始化一个对象，上面的代码可以改写成为提下形式：   
``` node.js
var buffer = Buffer.from([0x48,0x65,0x6c,0x6c,0x6c,0x6f,0x20,0x4e,0x64f,0x64,0x65]);//"Hellow Node"
var buffer = new Buffer.from("Hellow Node");
console.log(buffer);
//结果：<Buffer 48 65 6c 6f 20 4e 6f 64 65>
```   
如果想把一个Buffer对象转换成字符串的形式，需要用到toString()方法，调用格式为：  
``` node.js
buffer。toString([encoding],[start],[end]);
encoding:目标编码格式
start:起始位置
end:结束位置
```   
Bufer支持的编码格式有限，只有以下六种：
1. ASCⅡ
2. Base64
3. Binary
4. hex
5. UTF-8
6. UTF-16LE/UCS-2  

buffer还提供了isEncoding方法来判断是否支持转换为目标编码格式。   

例如：把“Hellow Node”的Buffer对象转换为字符串，可以这样调用：    
``` node.js
//制转换前五个字符 输出“hello”
console.log(buffer.tiString("utf-8",0,5));
```   
### Buffer 的拼接

Buffer一个常见的场景是用来处理HTTP的post请求，例如下面代码:  
``` node.js
var body = '';
req.setEncoding("utf-8");
req.on("data",function(chunk){
    body += chunk;
});
req.on("end",fiunction(){
});
```   
上面代码使用+=来拼接上传的数据流，这个过程包含了一个隐式的编码转换。  
body += chunk 相当于 body+=chunk。toString()，当上传的字符全是英文字符的时候固然没有问题，但如果包含中文或者其他语言，由于toString方法默认使用UTF-8编码，这个时候就可能出现乱码。
```   
举个例子：首先构造一个中文字符串，并保存为test.txt      
八百标兵奔北坡，北坡炮兵并排跑。炮兵排把标兵碰，标兵怕碰炮兵炮。  
``` node.js
var rs =require("fs").createReadStream("test.txt",{highWaterMark :10});
var data = "";
rs.on("data",function (chunk){
    data += chunk;
});
rs.on("end",function(){
    console.log(data);
});
```   
**highWaterMark**    
字面的意思最高水位线,它表示内部缓冲区最多能容纳的字节数，如果超过这个大小，就停止读取资源文件，默认大小64KB。  
假设文件的大小超过默认值64KB就会触发data事件：chunk的大小就等于*highWaterMark*大小;直到文件读取完成时，触发end事件。    
由于UTF-8中一个汉字占三个字节，那么highWaterMark设置为10，每三个子之后就有一个字会被截段，因此在调用tostring方法的时候出现乱码。  
目前上面的代码已经被舍弃，官方推荐使用push方法来拼接Buffer，如下面代码所示：  
``` node.js
var rs =require("fs").createReadStream("test.txt",{highWaterMark :10});
var data = [];
rs.on("data",function (chunk){
    data.push(chunk);
});
rs.on("end",function(){
    var buf = Buffer.concat(data);
    console.log(buf.toString());
});
```  
上面代码在拼接的过程中不会有隐式的编码转换，首先将Buffer放到数组里面去，等待传输完后在进行转换，这样就不会出现乱码。