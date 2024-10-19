[学习的网站](https://css.bqrdh.com/triangle/editor)


绘制三角形其实就是利用`border`属性来绘制

```css
<div class="triangle"></div>

<style>
/* 分别给每个边框设置不同的颜色 */
    .triangle{
        width: 100px;
        height: 100px;
        background: #ccc;
        border: 20px solid #ccc;
        border-top-color: red;
        border-right-color: chocolate;
        border-bottom-color: black;
        border-left-color: blue;
    }
</style>
```

<div class="triangle1"></div>

<style>
    .triangle1 {
        width: 100px;
        height: 100px;
        background: #ccc;
        border: 20px solid #ccc;
        border-top-color: red;
        border-right-color: chocolate;
        border-bottom-color: black;
        border-left-color: blue;
    }
</style>


**如果把div的宽高设置为0，然后调整上下左右边框距离**  

```css
.triangle2,.triangle3,.triangle4,.triangle5,.triangle6,.triangle7{
        margin-right:10px;
        width: 0;
        height: 0;
        display: inline-block;
    }
    .triangle2 {
        border: 50px solid #ccc;
        border-top-color: red;
        border-right-color: chocolate;
        border-bottom-color: black;
        border-left-color: blue;
    }
    .triangle3 {
        border-top: 70px solid red;
        border-right: 40px solid chocolate;
        border-bottom: 30px solid black;
        border-left: 60px solid blue;
        
    }
    .triangle4 {
        border-right: 30px solid chocolate;
        border-bottom: 100px solid black;
        border-left: 70px solid blue;
    }
    .triangle5 {    
        border-top: 100px solid red;
        border-right: 100px solid chocolate;
    }
    .triangle6 {    
        border: 50px double #ccc;
        border-top-color: red;
        border-right-color: chocolate;
        border-bottom-color: black;
        border-left-color: blue;
    }
    .triangle7 {   
        box-shadow: 5px -5px 0px 5px #ff0000;
        border-top: 60px solid #ff0000;
        border-right: 60px solid #ff0000;
        border-bottom: 30px solid blue;
        border-left: 30px solid blue
    }
```

<div class="triangle2"></div>
<div class="triangle3"></div>
<div class="triangle4"></div>
<div class="triangle5"></div>
<div class="triangle6"></div>
<div class="triangle7"></div>

<style>
    .triangle2,.triangle3,.triangle4,.triangle5,.triangle6,.triangle7{
        margin-right:10px;
        width: 0;
        height: 0;
        display: inline-block;
    }
    .triangle2 {
        border: 50px solid #ccc;
        border-top-color: red;
        border-right-color: chocolate;
        border-bottom-color: black;
        border-left-color: blue;
    }
    .triangle3 {
        border-top: 70px solid red;
        border-right: 40px solid chocolate;
        border-bottom: 30px solid black;
        border-left: 60px solid blue;
        
    }
    .triangle4 {
        border-right: 30px solid chocolate;
        border-bottom: 100px solid black;
        border-left: 70px solid blue;
    }
    .triangle5 {    
        border-top: 100px solid red;
        border-right: 100px solid chocolate;
    }
    .triangle6 {    
        border: 50px double #ccc;
        border-top-color: red;
        border-right-color: chocolate;
        border-bottom-color: black;
        border-left-color: blue;
    }
    .triangle7 {   
        box-shadow: 5px -5px 0px 5px #ff0000;
        border-top: 60px solid #ff0000;
        border-right: 60px solid #ff0000;
        border-bottom: 30px solid blue;
        border-left: 30px solid blue
    }
</style>


**已经能看到三角形了，我们把不需要的边使用`transparent`设置透明颜色**

```css
border: 50px solid transparent;
border-top-color: red;
```

<div class="triangle10"></div>

<style>
    .triangle10 {
        width: 0;
        height: 0;
        border: 50px solid transparent;
        border-top-color: red;
    }
</style>

现在三角形已经可以看出来，而且四个方向都行。    

> 小知识：如果加一个圆角，可以出来一个扇形。

<div class="triangle11"></div>

<style>
    .triangle11 {
        width: 0;
        height: 0;
        border: 50px solid transparent;
        border-top-color: red;
        border-radius: 50%;
    }
</style>