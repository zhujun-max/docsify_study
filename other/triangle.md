[学习的网站](https://css.bqrdh.com/triangle/editor)


?> 三角形原理其实是利用`border`属性的颜色与宽高绘制。




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

**如果把div的宽高设置为0，然后给边框设置距离**  
<div class="triangle20"></div>

<style>
    .triangle20 {
        width: 0;
        height: 0;
        background: #ccc;
        border: 20px solid #ccc;
        border-top-color: red;
        border-right-color: chocolate;
        border-bottom-color: black;
        border-left-color: blue;
    }
</style>

```css
<div class="triangle20"></div>

<style>
    .triangle20 {
        width: 0;
        height: 0;
        background: #ccc;
        border: 20px solid #ccc;
        border-top-color: red;
        border-right-color: chocolate;
        border-bottom-color: black;
        border-left-color: blue;
    }
</style>
```




**稍微复杂一些的三角形**

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

**把不需要的边使用`transparent`设置透明颜色**

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
  

**如果加一个圆角，可以出来一个扇形**

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

**空心三角形，就是两个div重叠在一起，也可以使用clip-path**
<div class="triangle12"></div>

<style>
.triangle12 {
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 0 50px 50px;
  border-color: transparent transparent #d9534f;
  position: relative;
}
.triangle12:after {
  content: '';
  border-style: solid;
  border-width: 0 40px 40px;
  border-color: transparent transparent #fff;
  position: absolute;
  top: 6px;
  left: -40px;
}
</style>
