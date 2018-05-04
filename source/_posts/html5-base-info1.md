---
title: htnl5_base_info1
date: 2018-04-09 10:00:29
tags: [HTML5]
categories: 童长钱
description: Html5 
---

## 什么是HTML5

HTML 5草案的前身名为Web Applications 1.0，是在2004年由WHATWG提出，再于2007年获W3C接纳，并成立了新的HTML工作团队。在2008年1月22日，第一份正式草案发布。WHATWG表示该规范是目前仍在进行的工作，仍须多年的努力。目前Firefox、Google Chrome、Opera、Safari（版本4以上）、Internet Explorer 9已支援HTML5技术。

HTML5本质并没有对之前HTML4版本的规范进行彻底的变革，而是一开始设计就考虑了跟之前的标准进行兼容，并且把最新的WEB开发的一些新技术新的规范引入进了新版本的标准中。

<!--more-->
## HTML5新特性

### 新增拥有具体含义的标签

现在所有的站点基本上都是div+css布局，几乎所有的文章标题、内容、辅助介绍等都用div容器来承载。搜索引擎在抓取页面内容时，因为没有明确的容器的含义只能去猜测这些标签容器承载的是文章标题还是文章内容等。HTML5新标准中直接添加了拥有具体含义的HTML标签比如：**article**、**footer**、**header**、**nav**、**section**

### 新增更加智能的表单类型

之前的表单标签仅仅是简单的类型的约束，比如文本框、文本域、下拉列表等。而跟业务结合紧密的表单标签数据校验等控制都没有很好的支持，基本上都是跟第三方的JS控件进行结合使用，但是这些第三方总会涉及到版本控制、浏览器兼容性、非标准等一系列的问题。而在HTML5的标准中直接添加了智能表单，让这一切都变得那么的简单，比如 *calendar*、*date*、*time*、*email*、*url*、*search*

### 让Web程序更加的独立，减少了对第三方插件的依赖。

在HTML5标准中原生的就支持音频、视频、画布等技术。让WEB程序更加独立，更好的适应多种形式的客户端。

### 对本地离线存储的更好的支持

HTML5 提供了两种在客户端存储数据的新方法：

*localStorage* - 没有时间限制的数据存储  
*sessionStorage* - 针对一个 session 的数据存储
### HTML5即时二维绘图 ,既画布的引入

HTML5 的canvas元素使用 JavaScript 在网页上绘制图像。并拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。

### JS支持多线程

在不影响UI update及浏览器与用户交互的情况下, 前端做大规模运算，只能通过 setTimeout 之类的去模拟多线程 。而新的标准中，JS新增的HTML5 Web Worker对象原生的就支持多线程。

### WebSockets让跨域请求、长连接、数据推送变得简单

*WebSockets*是在一个(TCP)接口进行双向通信的技术，*PUSH*技术类型。WebSocket是html5规范新引入的功能，用于解决浏览器与后台服务器双向通讯的问题，使用WebSocket技术，后台可以随时向前端推送消息，以保证前后台状态统一，在传统的无状态HTTP协议中，这是“无法做到”的。

### 更好的异常处理

HTML5(text/html)浏览器将在错误语法的处理上更加灵活。HTML5在设计时保证旧的浏览器能够安全地忽略掉新的HTML5代码。与HTML4.01相比，HTML5给出了解析的完整规则，让不同的浏览器即使在发生语法错误时也能返回完全相同的结果。

### 文件API让文件上传和操纵文件变得那么简单

由于项目中经常遇到用Web应用中控制操作本地文件，而之前都是使用一些富客户端技术比如*flash*，*ActiveX*，*Silverlight*等技术。在HTML5的新的提供的 HTML5 File API 让JS可以轻松上阵了。

## HTML5与HTML4的区别

### 取消了一些过时的HTML4的标签

其中包括纯粹显示效果的标记，如font和center，它们已经被 CSS完全取代。

其他取消的属性:~~acronym~~, ~~applet~~, ~~basefont~~, ~~big~~,~~center~~, ~~dir~~, ~~font~~, ~~frame~~,~~frameset~~, ~~isindex~~, ~~noframes~~, ~~strike~~,~~tt~~

### 添加了一些新的元素
更加智能的表单元素：*date*, *email*, *url*等; 更加合理的标签：**section**, **video**, **progress**, **nav**, **meter**, **time**, **, **canvas** 等。

### 文件类型声明

1.仅有一种类型
``` html
<!DOCTYPE html>
```
 **不懂的地方可以参考 [http://www.w3cSchool.com](http://www.w3cSchool.com "w3")或者百度搜索[http://www.baidu.com](http://www.baidu.com "www.baidu.com")**

 ———END
