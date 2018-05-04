---
title: Html5_canvas_2
date: 2018-04-18
tags: [HTML5]
categories: 童长钱
description: Html5-ccanvas进阶 canvas绘制 组合图形
---


## canvas 画布相关知识进阶  
### 1. canvas注意事项  
**canvas是基于状态绘图**  
**canvas绘图会使用到坐标系**   
**坐标系**：*原点在画布四个角的左上角，沿着左上角水平方向为x轴正方向，沿着左上角竖直向下是y轴的正方向*

<!--more-->
###  2. canvas是状态绘图 

``` html
//空三角形
function sanjiaoxing() {
    ctx.beginPath()
    ctx.moveTo(100, 100)
    ctx.lineTo(666, 500)
    ctx.lineTo(100, 500)
    ctx.lineTo(100, 100)
    ctx.closePath()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "#ff5421";
    ctx.stroke()
}

//填充描边三角形
function sanjiaoxing1() {
    ctx.beginPath()
    ctx.moveTo(200, 100)
    ctx.lineTo(800, 200)
    ctx.lineTo(800, 300)
    ctx.lineTo(200, 100)
    ctx.closePath()
    ctx.fillStyle = "rgb(2,100,60)";
    ctx.fill()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "red";
    ctx.stroke()
}
 ```
 
    在上面的代码中ctx.moveTo(100, 100)和  ctx.lineTo(666, 500) 描述的都是一个状态。  

    **通俗的来讲** 
    ctx.moveTo(100, 100)
    是把笔尖定位到坐标系（100,100）这个位置
    ctx.lineTo(666, 500)是把笔尖移动到坐标系中的（666，500）这个点
    ctx.closePath()这个方法在路径绘制成后，指向终点。
    如果绘制的是线段，并且未形成封闭的图形，且与  
    ctx.moveTo(100,100)点创建的有一定的平面大小
    在调用ctx.stroke()方法时
    画出来的只是线段
    如果调用ctx.fill()会把绘制路径所围成区域填充满
    前提要使用  ctx.fillStyle = "rgb(2,100,60)";设置颜色
    颜色默认绘制的都是黑色。

 ### 绘制图案
 **七巧板代码-自己画的**
 ```七巧板
 function qqb1() {
    ctx.beginPath()
    ctx.moveTo(0, 0)
    ctx.lineTo(0, 0)
    ctx.lineTo(400, 0)
    ctx.lineTo(200, 200)
    ctx.closePath()
    ctx.fillStyle = "rgb(255,0,0)";
    ctx.fill()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "black";
    ctx.stroke()
}
function qqb2() {
    ctx.beginPath()
    ctx.moveTo(0, 0)
    ctx.lineTo(0, 0)
    ctx.lineTo(0, 400)
    ctx.lineTo(200, 200)
    ctx.closePath()
    ctx.fillStyle = "rgb(125,1125,0)";
    ctx.fill()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "black";
    ctx.stroke()
}
function qqb3() {
    ctx.beginPath()
    ctx.moveTo(400, 0)
    ctx.lineTo(400, 0)
    ctx.lineTo(400, 200)
    ctx.lineTo(300, 300)
    ctx.lineTo(300, 100)
    ctx.closePath()
    ctx.fillStyle = "rgb(0,255,125)";
    ctx.fill()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "black";
    ctx.stroke()
}
function qqb4() {
    ctx.beginPath()
    ctx.moveTo(300, 300)
    ctx.lineTo(300, 300)
    ctx.lineTo(300, 100)
    ctx.lineTo(200, 200)
    ctx.closePath()
    ctx.fillStyle = "rgb(125,0,125)";
    ctx.fill()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "black";
    ctx.stroke()
}
function qqb5() {
    ctx.beginPath()
    ctx.moveTo(300, 300)
    ctx.lineTo(300, 300)
    ctx.lineTo(200, 200)
    ctx.lineTo(100, 300)
    ctx.lineTo(200, 400)
    ctx.closePath()
    ctx.fillStyle = "rgb(255,100,60)";
    ctx.fill()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "black";
    ctx.stroke()
}

function qqb6() {
    ctx.beginPath()
    ctx.moveTo(0, 400)
    ctx.lineTo(200, 400)
    ctx.lineTo(100, 300)
    ctx.closePath()
    ctx.fillStyle = "rgb(0,256,125)";
    ctx.fill()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "black";
    ctx.stroke()
}

function qqb7() {
    ctx.beginPath()
    ctx.moveTo(200, 400)
    ctx.lineTo(200, 400)
    ctx.lineTo(400, 200)
    ctx.lineTo(400, 400)
    ctx.closePath()
    ctx.fillStyle = "rgb(125,255,0)";
    ctx.fill()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "black";
    ctx.stroke()
}
 ```
 **七巧板代码-copy的**
 ```七巧板
 var param = [
    { p: [{ x: 0, y: 0 }, { x: 400, y: 0 }, { x: 200, y: 200 }], color: "red" },
    { p: [{ x: 0, y: 0 }, { x: 0, y: 400 }, { x: 200, y: 200 }], color: "#ff6521" },
    { p: [{ x: 400, y: 0 }, { x: 400, y: 200 }, { x: 300, y: 100 }], color: "#a7abb2" },
    { p: [{ x: 300, y: 100 }, { x: 400, y: 200 }, { x: 300, y: 300 }, { x: 200, y: 200 }], color: "#00ccbb" },
    { p: [{ x: 200, y: 200 }, { x: 300, y: 300 }, { x: 100, y: 300 }], color: "#ffff00" },
    { p: [{ x: 100, y: 300 }, { x: 300, y: 300 }, { x: 200, y: 400 }, { x: 0, y: 400 }], color: "#ff00ff" },
    { p: [{ x: 200, y: 400 }, { x: 400, y: 400 }, { x: 400, y: 200 }], color: "#000ff0" }
];
function qiqiaoban() {
    for (i = 0; i < param.length; i++) {
        darw(param[i], ctx)
    }
}
function darw(param, ctx) {
    ctx.beginPath()
    ctx.moveTo(param.p[0].x, param.p[0].y)
    for (k = 0; k < param.p.length; k++) {
        ctx.lineTo(param.p[k].x, param.p[k].y)
    }
    ctx.closePath()
    ctx.fillStyle = param.color;
    ctx.fill()
    ctx.lineWidth = 5;
    ctx.strokeStyle = "black";
    ctx.stroke() 
}
```
### 倒计时表（最长时间在24小时内）
**数字和符号的点阵，用canvas绘制的点阵**
```js
digit =
    [
        [
            [0,0,1,1,1,0,0],
            [0,1,1,0,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,0,1,1,0],
            [0,0,1,1,1,0,0]
        ],//0
        [
            [0,0,0,1,1,0,0],
            [0,1,1,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [1,1,1,1,1,1,1]
        ],//1
        [
            [0,1,1,1,1,1,0],
            [1,1,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,0,0],
            [0,0,1,1,0,0,0],
            [0,1,1,0,0,0,0],
            [1,1,0,0,0,0,0],
            [1,1,0,0,0,1,1],
            [1,1,1,1,1,1,1]
        ],//2
        [
            [1,1,1,1,1,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,0,0],
            [0,0,1,1,1,0,0],
            [0,0,0,0,1,1,0],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0]
        ],//3
        [
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,1,0],
            [0,0,1,1,1,1,0],
            [0,1,1,0,1,1,0],
            [1,1,0,0,1,1,0],
            [1,1,1,1,1,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,0,1,1,0],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,1,1]
        ],//4
        [
            [1,1,1,1,1,1,1],
            [1,1,0,0,0,0,0],
            [1,1,0,0,0,0,0],
            [1,1,1,1,1,1,0],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0]
        ],//5
        [
            [0,0,0,0,1,1,0],
            [0,0,1,1,0,0,0],
            [0,1,1,0,0,0,0],
            [1,1,0,0,0,0,0],
            [1,1,0,1,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0]
        ],//6
        [
            [1,1,1,1,1,1,1],
            [1,1,0,0,0,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,1,1,0,0,0],
            [0,0,1,1,0,0,0],
            [0,0,1,1,0,0,0],
            [0,0,1,1,0,0,0]
        ],//7
        [
            [0,1,1,1,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0]
        ],//8
        [
            [0,1,1,1,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,0,0],
            [0,1,1,0,0,0,0]
        ],//9
        [
            [0,0,0,0],
            [0,0,0,0],
            [0,1,1,0],
            [0,1,1,0],
            [0,0,0,0],
            [0,0,0,0],
            [0,1,1,0],
            [0,1,1,0],
            [0,0,0,0],
            [0,0,0,0]
        ]//:
    ];
```
**js绘制图像和倒计时逻辑代码脚本代码**
```js
var WINDOW_WIDTH = 1024;
var WINDOW_HEIGHT = 768;
var RADIUS = 8;
var MARGIN_TOP = 60;
var MARGIN_LEFT = 30;

var canvas = document.getElementById('canvas');
var context = canvas.getContext("2d");
const endTime = new Date(2018,3,18,10,47,52);
var curShowTimeSeconds = 0

window.onload = function(){
    canvas.width = WINDOW_WIDTH;
    canvas.height = WINDOW_HEIGHT;
    curShowTimeSeconds = getCurrentShowTimeSeconds()
    render( context )
}
function darw(){
    canvas.width = WINDOW_WIDTH;
    canvas.height = WINDOW_HEIGHT;
    curShowTimeSeconds = getCurrentShowTimeSeconds()
    render( context )
}
function getCurrentShowTimeSeconds() {
    var curTime = new Date();
    var ret = endTime.getTime() - curTime.getTime();
    ret = Math.round( ret/1000 )
    return ret >= 0 ? ret : 0;
}

function render( cxt ){
    var hours = parseInt( curShowTimeSeconds / 3600);
    var minutes = parseInt( (curShowTimeSeconds - hours * 3600)/60 )
    var seconds = curShowTimeSeconds % 60

    renderDigit( MARGIN_LEFT , MARGIN_TOP , parseInt(hours/10) , cxt )
    renderDigit( MARGIN_LEFT + 15*(RADIUS+1) , MARGIN_TOP , parseInt(hours%10) , cxt )
    renderDigit( MARGIN_LEFT + 30*(RADIUS + 1) , MARGIN_TOP , 10 , cxt )
    renderDigit( MARGIN_LEFT + 39*(RADIUS+1) , MARGIN_TOP , parseInt(minutes/10) , cxt);
    renderDigit( MARGIN_LEFT + 54*(RADIUS+1) , MARGIN_TOP , parseInt(minutes%10) , cxt);
    renderDigit( MARGIN_LEFT + 69*(RADIUS+1) , MARGIN_TOP , 10 , cxt);
    renderDigit( MARGIN_LEFT + 78*(RADIUS+1) , MARGIN_TOP , parseInt(seconds/10) , cxt);
    renderDigit( MARGIN_LEFT + 93*(RADIUS+1) , MARGIN_TOP , parseInt(seconds%10) , cxt);
}

function renderDigit( x , y , num , cxt ){
    cxt.fillStyle = "rgb(0,102,153)";
    for( var i = 0 ; i < digit[num].length ; i ++ ){
        for(var j = 0 ; j < digit[num][i].length ; j ++ ){
            if( digit[num][i][j] == 1 ){
                cxt.beginPath();
                cxt.arc( x+j*2*(RADIUS+1)+(RADIUS+1) , y+i*2*(RADIUS+1)+(RADIUS+1) , RADIUS , 0 , 2*Math.PI )
                cxt.closePath()
                cxt.fill()
            }
		}
	}
}
setInterval(darw, 1000);
注意事项：
*const endTime = new Date(2018,3,18,10,47,52);*
**月份是从0开始，到11结束共12个月**
```

