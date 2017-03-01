#### 浏览器支持情况  
IE9完全不支持，其他只需要添加-webkit-前缀。  
于IE10/11来说，我们无法对立方体自身施加3D变换，     
### 需要用到相关的css属性  
perspective:1000；3d透视  
transform-style: preserve-3d/flat; 容器以3d效果显示  
transform：translateZ(100px);在3d坐标中向各个方向移动
### 一般情况下的模板
```
<div class="stage"> //设置3d透视，作为舞台
     <div class="container>  //设置preserv-3d，容器子元素以3d效果展示
         <div></div> //子元素
         <div></div>
         <div></div>
     </div>
</div>
```
#### 下面就是一个具体的实例
 * 先构造模板
 ```
    <div class="stage">
          <div class="container">
             <div class="slide slide1"></div>
             <div class="slide slide2"></div>
             <div class="slide slide3"></div>
             <div class="slide slide4"></div>
             <div class="slide slide5"></div>
             <div class="slide slide6"></div>
          </div>
     </div>
```
* css部分设置
* stage舞台，主要是设置==3d透视效果==  
```
.stage{ perspective:1000px; }

```
* container容器，设置容器内部以3d效果显示
```
.container{
     position:relative;
     transform-style: preserve-3d;
     animation: lf 6s linear infinite alternate;
}
```
* 各个面的具体位置设置  
注意：各个元素的旋转点默认是中点，transform-origin可以改变变换点
```
  .slide{
      position:absolute; /*<!--可以用transform:translate属性设置位置-->*/
      width:300px;
      height: 300px;
      line-height:300px;
      color:#fff;
      text-align: center;
    }
    .slide1{
      transform: translateY(-150px) rotateX(90deg);
      background:rgb(41, 150, 75);
    }
    .slide2{
       transform: translateY(150px) rotateX(90deg);
      background: rgb(164, 222, 22);
    }
    .slide3{
    transform:  translateX(-150px) rotateY(90deg);
      background:rgb(37, 75, 209);
    }
    .slide4{
     transform: translateX(150px) rotateY(90deg);
      background: rgb(31, 224, 216);
    }
    .slide5{
       transform: translateZ(150px);
      background: rgb(197, 255, 3);
    }
    .slide6{
      transform: translateZ(-150px);
      background: rgb(5, 240, 229);
    }
```
加入动画后效果如下：

* 个人最重要的有两点，一是构造3d效果的舞台容器模板，另一个是就是理解旋转位移在3d坐标中的原理，就可以构造出自己想要的图形。 

### 3d立体相册
* 基本流程和3d立方体相同，不同点是在旋转位移不同，构造出图像不同
#### 基本的模板
```
 <div class="stage">
     <div class="container">
         <div class="slide slide1"></div>
         <div class="slide slide2"></div>
         <div class="slide slide3"></div>
         <div class="slide slide4"></div>
         <div class="slide slide5"></div>
         <div class="slide slide6"></div>
     </div>
</div>
```
* 舞台和容器的样式几乎一样，不过在设置perspective3d透视的大小时，需要根据图像的实际情况设置，遵循近大远小  
```
   .stage{
     perspective: 1500px;

   }
   .container{
     transform-style: preserve-3d;
     width:400px;
     height: 400px;
     margin:50px auto;
     position: relative;
     /*transform-origin: */
   }
```
* 最后是设置各个各个子元素的样式  
1、根据图片的张数确定图片之间的角度间隔，然后设置图片围绕y轴  
2、在设置每张图片向各自的z轴移动大于图片宽度的距离
* 具体css
```css
   .slide{
     position: absolute;
     width: 300px;
     height: 300px;
     top:100px;
     left:100px;
   }
   .slide1{
     background: url(img/1.jpg) no-repeat;
     background-size: cover;
     transform:rotateY(0deg) translateZ(400px);
   }
   .slide2{
     background: url(img/2.jpg) no-repeat;
     background-size: cover;
     transform:rotateY(60deg) translateZ(400px);
   }
   .slide3{
     background: url(img/3.jpg) no-repeat;
     background-size: cover;
     transform:rotateY(120deg) translateZ(400px);
   }
   .slide4{
     background: url(img/4.jpg) no-repeat;
     background-size: cover;
     transform:rotateY(180deg) translateZ(400px);
   }
   .slide5{
     background: url(img/5.jpg) no-repeat;
     background-size: cover;
     transform:rotateY(240deg) translateZ(400px);
   }
   .slide6{
     background: url(img/6.jpg) no-repeat;
     background-size: cover;
     transform:rotateY(300deg) translateZ(400px);
   }
```
<div class="stage">
 <div class="container">
     <div class="slide slide1"></div>
     <div class="slide slide2"></div>
     <div class="slide slide3"></div>
     <div class="slide slide4"></div>
     <div class="slide slide5"></div>
     <div class="slide slide6"></div>
    </div>
 </div>

