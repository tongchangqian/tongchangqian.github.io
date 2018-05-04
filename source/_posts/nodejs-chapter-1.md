---
title: nodejs-chapter-1
date: 2018-04-25
tags: [nodejs]
categories: 童长钱
description: nodejs 常用模块 文件引入和使用 this的用法
---

#### 1.1、 JavaScript的模块规范  
目前流行的JavaScript的模块规范主要有两种：  
**CommonJS**  
*CommonJS*把每一个文件看做一个模块，模块内部定义的每一个变量都是私有的，无法别其他模块使用，除非使用预定义的方法将内部定义的变量暴露出来（*通过exprots和require关键字来实现*）  
*CommonJS* 一个显著的特点就是模块加载是同步的，就目前来说，受限制于宽带速度，并不适用于浏览器中的人JavaScript。  
**AMD**  
*AMD*是Asynchronous Module Definition的缩写，意思就是“一步模块定义”，它采用异步方式加载模块，模块加载不影响它后面语句的运行。依赖这个模块代码定义在一个回调函数中，等到加载完成之后，这个回调才会运行。  
<!--more-->
#### 1.2、require及其运行机制  

``` node.js
//preson.js
var preson ={
    talk: function () {
        console.log("I am talking..."); 
    },
    listen :function () {
        console.log("I am listening..."); 
    }
    //MORE func...
}
module.exports = person;
```  

这样实现一个自定义的模块，该模提供的一个preson接口，然后使用module.exports将接口口暴露给外部有使用，外部的代码想要使用preson.js的方法，需要使用require关键字引入该接口。  

```node.js
var persom =requitr("./person.js");
person.talk();
```  

**注意**：再引入自定义模块时省略相对路径“./”会导致错误。  
如果只需要引入其中的人一个，代码可以这样写：  

```node.js
var talk =require("./person.js").talk;
talk();
```  

**require**关键字并不依赖于exports，应为加载一个没有暴露任何方法的模块，这相当于执行一个模块代码，这样做通常是没有意义的。   

#### 1.3、require的缓存策略  

Node会自动缓存require引入的文件，使得下次再引入不需要在经过文件系统而是直接从缓存读取。这种缓存是基于文件路径定位的，这表示两个完全相同的文件，但在他们位于不同的路径下，也会在缓存中维持两份。例如使用下面代码访问目前在缓存中的文件：  

```node.js
var moudle =require("./moudle.js");
console.log(require.cache);
```

#### 1.4、require的隐患
当调用require加载一个模块时，模块内部的代码会被调用，有时候会带来隐藏的bug。例如下面的代码：  

```node.js
//module.js
function test(){
    setInterval(function (){
        console.log("test");
    }),100
}
test();
module.expoets =test;
//run.js
var test require("./module.js");
```
run.js除了加载一个模块之外没有进行任何操作，试着运行一下，就会发现每隔一秒钟就会输出一个 “test”字符串，同时run.js的进程不会退出。因为：加载一个模块相当于执行模块内部代码，在module.js中由于设置了一个不间断的定时器，导致run.js也会一直运行。 

#### 1.5、模块化下的作用域
主要关注点在**this**上。  
Node和javaScript中的this指向上有一些区别，其中Node控制台和脚本文件的策略不尽相同。对于浏览器中的javaScript来说，无论是在脚本还是在浏览器控制台中，其this的指向是一致的，然Node并非这样。
1. 控制台中的this

``` nodejs
console.log(this);
//输出：window{stop:functiom,open function,.....}
//---------------------
var a = 10;
console.log(this.a);
//输出 10;
```
2. Node控制台中的this
在node控制台中,全局变量会挂到global下.  
创建一个test.js文件在文件中添加以下代码：
``` nodejs
console.log(this);//{}
```
运行 node test.js打印出结果是一个空对象。
执行下面代码：
``` nodejs
var a = 10;
console.log(this.a);//undefined
console.log(global.a);//undefined
```
结果全部都是undefined,说明定义的变量a并没有挂到全局变量的this或者global对象。  
然而如果声明变量时不使用var或者let关键字修饰，例如下面代码：
``` nodejs
a = 10;
console.log(global.a);//10
```
这样却可以正常打印结果。
node脚本文件中定义的全局this指向是：module.exports。如下面代码所示：

``` nodejs
this.a = 10;
console.log(module.exports);//10
```
#### 1.6、Node中作用域种类
1. 全局作用域
``` nodejs
a = 10;
console.log(global.a);//10
```
2. 模块作用域
``` nodejs
this.a = 10;
console.log(module.exports);//10
```
3. 函数作用域  
这个大家都比较熟悉，就不在介绍。  

4. 块级作用域  
ES2015中引入let关键字提供了对块级作用域的支持。