---
title: canvas使用
date: 2017-02-22 16:02:07
tags: 学习 css
---
### 1.canvas基本用法
##### canvasa.getContext('2d')获取设备上下文
> * "webg1" 代表三维渲染上下文
> * "webg12" 代表创建一个支持webGL版本2的浏览器
==设备上下文中还可以设置具体属性，详见[MDN的HTMLCanvasElement.getContext()](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCanvasElement/getContext)
##### 基本模板

```
<html>
  <head>
    <title>Canvas tutorial</title>
    <script type="text/javascript">
      function draw(){
        var canvas = document.getElementById('tutorial');//获取canvas节点
        if (canvas.getContext){
          var ctx = canvas.getContext('2d');//设置2d上下文
        }
      }
    </script>
    <style type="text/css">
      canvas { border: 1px solid black; }
    </style>
  </head>
  <body onload="draw();">
    <canvas id="tutorial" width="150" height="150"></canvas>
  </body>
</html>
```
 <!--more-->
##### canvas绘制图形

**画布栅格**，canvas被默认的网格所覆盖，左上角为原点（0，0)。x轴向右，y轴向下  
canvas元素只支持一种原生的图形绘制
```
fillRect(x,y,widht,heigth) //绘制一个填充矩形
strokeRect(x,y,widht,height) //绘制一个矩形框架
clearRect(x,y,widht,heigth) //清除指定矩形区域
```
**绘制路径**：其他的图形需要通过绘制一个闭合的路径，然后进行描边或填充区域
- 首先，你需要创建路径起始点。
- 然后你使用画图命令去画出路径。
- 之后你把路径封闭。
- 一旦路径生成，你就能通过描边或填充路径区域来渲染图形  
**相应函数**  
beginpath()新建一条路径   
closePaht() 闭合路径之后图形绘制命令又重新指向上下文中  
stroke()  通过线条来绘制轮廓
fill()  填充路径  
==注意：当前路径为空，即调用beginPath()之后，或者canvas刚建的时候，第一条路径构造命令通常被视为是moveTo（），无论最后的是什么。出于这个原因，你几乎总是要在设置路径之后专门指定你的起始位置==   
  
**路径绘制方法**：  
- 直线：moveTo(x,y) lineTo()
- 圆弧：arc(x,y,radius,startAngle,endAngle,anticolwise) ==角度使用弧度表示(Math.PI/180)*degrees,x、y值可变==
- 圆弧2：arcTo(x1,y1,x2,y2,radius) 根据控制点和半径画一段圆弧
- quadraticCurveTo(cp1x, cp1y, x, y)
绘制贝塞尔曲线，cp1x,cp1y为控制点，x,y为结束点。
- bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)
绘制二次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点。
- 矩形：rect(x,y,width,height)
* 实例  
```    
ctx.beginPath();//开始绘制路径
ctx.moveTo(75,50); //使用moveTo()和lineTo(x,y)来绘制直线
ctx.lineTo(100,75);
ctx.lineTo(100,25);
ctx.fill(); // 最后填充或者 ctx.stroke()使用线条绘制轮廓
```
**Path2D对象**  
```
new Path2D() //创建空的Path对象
new Path2D(path) //克隆Path对象
new Paht(d)  //从SVG建立Path对象
//实例
 var rectangle = new Path2D();
    rectangle.rect(10, 10, 50, 50); //创建一个矩形路径并保存在Path2D对象中

    var circle = new Path2D();
    circle.moveTo(125, 35);
    circle.arc(100, 35, 25, 0, 2 * Math.PI);
    ctx.stroke(rectangle);
    ctx.fill(circle);
```
### 色彩colrs
* fillstyle=color 填充颜色
* strokeStyle=color 边框颜色
```
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  for (var i=0;i<6;i++){
    for (var j=0;j<6;j++){
      ctx.fillStyle = 'rgb(' + Math.floor(255-42.5*i) + ',' + 
                       Math.floor(255-42.5*j) + ',0)';
      ctx.fillRect(j*25,i*25,25,25);
    }
  }
}
```
透明度 Transparency  
 ctx.fillStyle = 'rgb(255,221,0)'
 
 ### 线型linestyle
 - lineWidth=value
 - lineCap=type //设置线条末端样式     butt/round(圆角)/square(超出部分)
 - lineJoin=type // round, bevel 和 miter。默认是 miter。 
 ### 渐变 Gradients
createLinearGradient(x1,y1,x2,y2)  //渐变起点(x1,y1)与终点(x2,y2)
```
var lineargradient = ctx.createLinearGradient(0,0,150,150);//创建渐变对象
lineargradient.addColorStop(0,'white');//设置颜色
lineargradient.addColorStop(1,'black');
```
### 图案样式 Patterns
```
createPattern(image, type)
该方法接受两个参数。Image 可以是一个 Image 对象的引用，或者另一个 canvas 对象。  
Type 必须是下面的字符串值之一：repeat，repeat-x，repeat-y 和 no-repeat
最后将创建的样式赋给fillstyle

function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  // 创建新 image 对象，用作图案
  var img = new Image();
  img.src = 'images/wallpaper.png';
  img.onload = function(){

    // 创建图案
    var ptrn = ctx.createPattern(img,'repeat');
    ctx.fillStyle = ptrn;
    ctx.fillRect(0,0,150,150);

  }
}




```


