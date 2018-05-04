---
title: html5-base-info2
date: 2018-03-29 19:01:01
tags: [HTML5]
categories: 童长钱
description: Html5 基础-初识标签和结构
---
## 一、HTML5语法

```html5
<!DOCTYPE html>
<html lang="zh-CN">
    <head>
        <meta charset="utf-8">
        <title>HTML5语法</title>
    </head>
    <body>
        <form>
        <input Type="checkbox" checked />
        <input Type="test" />
        <input TYpe="checkbox" checked />
        <INPUT TYPE="RADIO"/>
        <input></input> 
        </form>
    </body>
</html>
```
<!--more-->
1. **DOCTYPE及编码格式语言**
``` html
<!DOCTYPE html><!--声明：文档类型 ！h5就是怎么简单-->
    <html lang="zh-CN"><!--设置语言-->
    <meta charset="utf-8"><!--声明文档的编码格式-->  
    <!--  **大小写都可以<对大小写不敏感>（注意：开发中：一般，默认使用小写**-->
    <input Type="test"value="效果图" />
    <input TYpe="checkbox" checked />
    <INPUT TYPE="RADIO"/>
    <!--以上在html5中都是可以的.-->
```
3. *省略的标的标签*

1. *不允许些结束的标签* 
**are**,**baser**,**col**,**common**,**embed**,**hr**,**img**,**input**,**keygen**,**link**,**meat**,**param**,**source**,**tract**, **wbr**
2. *可以省略结束的标签*
**li**,**dt**,**dd**,**p**,**rt**,**optgroup**,**option**,**colgroup**,**thread**,**tbody**,**rt**,**td**,**th**
3. *完全可以省略的标签*
**html titlt tbody**

## 二、新增及删除标签  
一. **新增标签**
1. 结构标签
1.1、 **section** 表示页面中的一个内容区块，表示文档结构
1.2、 **article** 表示页面中一块与上下文不相关的独立核心内容，比如一篇文章
1.3、 **aside** 表示article内容之外的，与artice标签内容相关的辅助信息

2. 表单标签
**...**
3. 媒体标签
**video**,**audio**等
 
4. 其他标签
4.1、**mark**  高亮文本 
4.2、**progress**  进度条
4.3、**time** 时间"time datetime="2013-10-20T09:00Z" pubdate"9:00"/time"
4.4、**ruby**  文本解释
  
 二. **删除标签** > 1. 可以被css代替的标签
 2. 不再使用frame 3. 只有个别浏览器支持的标签
 4. 不常用的标签


**不懂的地方可以参考 [http://www.w3cSchool.com](http://www.w3cSchool.com "w3")或者百度搜索[http://www.baidu.com](http://www.baidu.com "www.baidu.com")**
