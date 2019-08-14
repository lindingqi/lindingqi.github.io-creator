---
title: "制作一个可以用鼠标拖动的div"
date: 2019-08-13T15:08:54+08:00
draft: false
---
# 我的第一个作品（js）
在观看方方老师的教学视频后，制作了一个小作品。在这里记录一些学习内容，以便日后的复习。
# 制作思路
实现的思路是这样的。先用js创建一个div，使用css的绝对定位，使样式中的top和left值发生变化，来实现div位置变化。鼠标拖动可以使用事件监听来实现，在onmousedown，onmousemove，onmouseup的时候实现不同的js代码，来完成鼠标拖动div。遇到bug时候，使用console方法去调试。
# 基本工作
## 在html中引入js
只需
```html
<script src="main.js"></script>
```
代码如下
```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>我的第一个js应用</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <script src="main.js"></script>
</body>

</html>
```
## 在js中创建div
需要在style.css中创建一个基本的div，并引入js中
style.css代码如下
```css
.demo{
     border:1px solid red;
   height: 100px;
   width: 100px;
   position: absolute;
   top:0;
   left:0;
}
body{
    margin: 0;
    height: 100vh;
    box-sizing: border-box
}
```
在js中引入只需要两条代码。如下
```js
let div1 = document.createElement('div');
document.body.appendChild(div1);
// 并指定
div1.className = 'demo'
```
# 相关js代码
```js
let div1 = document.createElement('div');
div1.className = 'demo'
div1.style.top = 'auto'

document.body.appendChild(div1);

var dragging = false
var lastX
var lastY

div1.onmousedown = function (e) {
    // 当鼠标按下时，才能移动，设置标记，记录下标记的初始位置
    dragging = true
    lastX = e.clientX
    lastY = e.clientY
}
document.onmousemove = function (e) {
    if (dragging === true) {
        // 获取移动差值
        var deltaX = e.clientX - lastX
        var deltaY = e.clientY - lastY
        // 由于js无法读取css初始top和left的值 ，设初始值为0
        var top = parseInt(div1.style.top) || 0
        var left = parseInt(div1.style.left) || 0
        div1.style.top = top + deltaY + 'px';
        div1.style.left = left + deltaX + 'px';
        // 移动的时候需要把最后一次值重置
        lastX = e.clientX
        lastY = e.clientY
    }
}

div1.onmouseup = function () {
    dragging = false
}
```