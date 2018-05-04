---
title: Html5-canvas_1
date: 2018-04-13 20:12:15
tags: [HTML5]
categories: 童长钱
description: Html5 canvas标签学习，制作canvas时钟
---

## canvas 

**w3c**:*canvas 元素用于在网页上绘制图形。* 

## 什么是 Canvas？ 

*HTML5 的 canvas 元素使用 JavaScript 在网页上绘制图像。画布是一个矩形区域，您可以控制其每一像素。canvas拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。*

<!--more-->
## html5创建画布

*在 html5中创建画布，并指定画布大小*
``` html
<canvas id="myCanvas"width="200"height="100"></canvas>
```
## 绘制图像 

*使用 JavaScript 来绘制图像，canvas 元素本身是没有绘图能力的。所有的绘制工作必须在。JavaScript 内部完成*
<!--more-->

``` html
下面代码 画一条直线：
var c=document.getElementById("myCanvas");
var cxt=c.getContext("2d");
cxt.moveTo(10,10);
cxt.lineTo(150,50);
cxt.stroke();
``` 

``` html
下面代码 画一个三角形：
var c=document.getElementById("myCanvas");
var cxt=c.getContext("2d");
cxt.moveTo(10,10);//把路径移动到画布中的指定点，不创建线条
cxt.lineTo(150,50);//添加一个新点，然后在画布中创建从该点到最后指定点的线条
cxt.lineTo(10,50);//添加一个新点，然后在画布中创建从该点到最后指定点的线条
closePath();//创建从当前点回到起始点的路径
``` 
``` html
下面代码绘制一个填充颜色为红色的矩形：
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="#FF0000";//设置颜色
ctx.fillRect(0,0,150,75)//画一个起点坐标（0，0）终点坐标（150,50）的矩形（有填充）
ctx.strokeRect(0,0,150,75);//画一个起点坐标（0，0）终点坐标（150,50）的矩形（无填充）
``` 
``` html
下面代码绘制一个圆形
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.arc(95,50,40,0,2*Math.PI);//圆心所在位置（X，y ），半径，幅度。
ctx.stroke();//绘制路径
``` 

## 下面是canvas画的一个简易时钟代码
``` html
html页面代码
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" >
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>canvas</title>
    <style type="text/css">
        div {
            text-align: center;
            margin-top: 250px;
        } 
        #appStudy{
            border:1px solid #cccccc;
        }
    </style>
</head>

<body>
    <div >
        <canvas id="app_study" ></canvas>
    </div>
    
    <script type="text/javascript" src="appStudy.js"></script>
</body>

</html>
脚本代码 
var dom = document.getElementById("clock");
var ctx = dom.getContext("2d");
var height = ctx.canvas.height;
var width = ctx.canvas.width;
var r = height / 2;
var rem = width / 200;
var ss = 0;
//表盘
function drawBackgroup() {
    ctx.save();
    ctx.translate(r, r);
    ctx.beginPath();
    ctx.lineWidth = 8 * rem;
    ctx.arc(0, 0, r - ctx.lineWidth, 2 * Math.PI, false);
    ctx.stroke();
    //画表盘数字
    var hourNumber = [3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 1, 2];
    ctx.font = 18 * rem + "px Arial";
    ctx.textAlign = "center";
    ctx.textBaseline = "middle"
    hourNumber.forEach(function (number, i) {
        var rad = 2 * Math.PI / 12 * i;
        var x = Math.cos(rad) * (r - 30 * rem);
        var y = Math.sin(rad) * (r - 30 * rem);
        ctx.fillText(number, x, y);
    });
    //刻度点
    for (var i = 0; i < 60; i++) {
        var rad = 2 * Math.PI / 60 * i;
        var x = Math.cos(rad) * (r - 18 * rem);
        var y = Math.sin(rad) * (r - 18 * rem);
        ctx.beginPath();

        if (i % 5 == 0) {
            ctx.fillStyle = "#000000";
            ctx.arc(x, y, 2 * rem, 0, 2 * Math.PI, false);
        } else {
            ctx.fillStyle = "#cccccc";
            ctx.arc(x, y, 2 * rem, 0, 2 * Math.PI, false);
        }
        ctx.fill();
    };
}
//时针
function drawHour(huor, min) {
    ctx.save();
    ctx.beginPath();
    ctx.fillStyle = "#000000";
    var sss = Math.PI / 360 * min;
    var hoss = 2 * Math.PI * huor / 12;
    ss = hoss + sss;
    ctx.rotate(ss);
    ctx.lineWidth = 3 * rem;
    ctx.lineCap = "round";
    ctx.moveTo(-6 * rem, 15 * rem)
    ctx.lineTo(6 * rem, 15 * rem);
    ctx.lineTo(2, -r / 2);
    ctx.lineTo(-2, -r / 2);
    ctx.fill();
    ctx.restore();
}
//分针
function drawMinute(min) {
    ctx.save();
    ctx.beginPath();
    ctx.fillStyle = "#000";
    ctx.rotate(2 * Math.PI * min / 60);
    ctx.lineWidth = 6 * rem;
    ctx.lineCap = "round";
    ctx.moveTo(-2 * rem, 40 * rem);
    ctx.lineTo(0, -r / 12 * 7);
    ctx.stroke();
    ctx.restore();
}
//秒针
function drawMiao(miao) {
    ctx.save();
    ctx.beginPath();
    ctx.fillStyle = "#ff0000";
    ctx.rotate(2 * Math.PI * miao / 60);
    ctx.lineWidth = 3 * rem;
    ctx.lineCap = "round";
    ctx.moveTo(-3 * rem, 45 * rem)
    ctx.lineTo(3 * rem, 45 * rem);
    ctx.lineTo(1, -r / 3 * 2);
    ctx.lineTo(-1, -r / 3 * 2);
    ctx.fill();
    ctx.restore();
}
//表中心点
function drawDot() {
    ctx.beginPath();
    ctx.fillStyle = "#fff";
    ctx.arc(0, 0, 2 * rem, 0, 2 * rem * Math.PI, false);
    ctx.fill();
    ctx.stroke();
}

function draw() {
    ctx.clearRect(0, 0, width, height);
    var nowTime = new Date();
    var hour = nowTime.getHours();
    var min = nowTime.getMinutes();
    var miao = nowTime.getSeconds();

    drawBackgroup();
    drawHour(hour, min);
    drawMinute(min);
    drawMiao(miao);
    drawDot();
    ctx.restore();
}
draw();
//定时器
setInterval(draw, 1000);
``` 

[canvas 属性参考地址](http://www.w3school.com.cn/tags/html_ref_canvas.asp)
