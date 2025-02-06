
## 一个div

[学习的网站](https://a.singlediv.com/)

### 所需知识点

#### 一、 background属性

+ `background-color`：设置元素的背景颜色，默认值：transparent。
+ `background-image`：设置元素的背景图像，默认值：none。
+ `background-size`：设置元素背景图像的大小，默认值：auto。
+ `background-position`：设置元素背景图像的位置，默认值：0% 0%。
+ `background-repeat`：设置背景图像是否重复，以及如何重复，默认值：repeat。
+ `background-clip`：设置元素背景的渲染区域，默认值：border-box。
+ `background-origin`：设置元素背景的定位区域（背景区），默认值：border-box。
+ `background-attachment`：设置元素的背景图像是否随页面滚动或固定，默认值：scroll。
+ `background-blend-mode`（不支持简写）：设置元素背景层的混合模式，默认值：normal。

#### 二、缩写规则

1. `color、image、size、position、repeat、attachment`。这六条属性值都不是必填项，不填会使用默认值。
2. `position / size`，定位属性必须要和大小在一起，使用`/`隔开。其余属性任意顺序。(如果只有一个参数，会作用在`position`上，如果要使用`size`，必须要填写为`position / size`)
3. `clip、origin`拥有三条相同的属性值，如果都没填写，就是用默认值。如果只填写了一个，将会同时作用于`clip、origin`。如果填写了两个，第一个为`origin`。第二个为`clip`。
4. 如果`background`属性设置了多个背景层，那么每个背景层之间使用`,`隔开。按顺序从前往后渲染。`color`始终在最底层显示，因为背景颜色是唯一的。

#### 三、可以填写多个参数的属性
```css
.streak{
    width: 100%;
    height: 150px;
    background-color: #eee;
    background-repeat: 
        no-repeat,
        repeat-x,
        no-repeat;
    background-image: 
        linear-gradient(yellow, yellow),
        linear-gradient(to right, #eee 0%, red 100%),
        radial-gradient(circle, red, yellow, green);
    background-size: 
        200px 40px,
        100px 40px,
        30px 30px;
    background-position: 
        left 10px top 10px,
        left 10px top 60px,
        left 10px top 110px;
}
```
<div class="streak"></div>
<style>
    .streak{
        width: 100%;
        height: 150px;
        background-color: #eee;
        background-repeat: 
            no-repeat,
            repeat-x,
            no-repeat;
        background-image: 
            linear-gradient(yellow, yellow),
            linear-gradient(to right, #eee 0%, red 100%),
            radial-gradient(circle, red, yellow, green);
        background-size: 
            200px 40px,
            100px 40px,
            30px 30px;
        background-position: 
            left 10px top 10px,
            left 10px top 60px,
            left 10px top 110px;
    }
</style>

```css
<style>
.ellipse{
    background-color: #f7f7f7;
    width:100%;
    height:200px;
    position: relative;
}
.ellipse > div {
    width: 220px;
    height: 60px;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-top: -30px;
    margin-left: -110px;
    border-radius: 2em;
    background-color: #3cb371;
    background-repeat: no-repeat;
    box-shadow: 
        inset 0 -.7em 1em .4em #919191, 
        0 0 0 .1em #008000;
    background: 
        radial-gradient(circle at 50% 100%, #008000 40%, rgba(0, 128, 0, 0) 40.5%) 20% 7% / 2em 1em,
        radial-gradient(circle at 50% 100%, #008000 40%, rgba(0, 128, 0, 0) 40.5%) 80% 11% / 1.5em .75em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 30% 30% / 1em 1em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 38% 35% / .6em .6em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 15% 50% / 1em 1em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 78% 33% / .6em .6em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 85% 40% / 1em 1em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 25% 60% / 1em 1em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 65% 50% / 1em 1em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 50% 70% / 1em 1em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 68% 65% / .6em .6em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 75% 70% / 1em 1em, 
        radial-gradient(circle at 50% 0, #008000 40%, rgba(0, 128, 0, 0) 40.5%) 35% 93% / 1.5em .75em,
        linear-gradient(to right, rgba(144, 238, 144, 0) 20%, rgba(144, 238, 144, 0.6) 40%, rgba(144, 238, 144, 0.6) 60%, rgba(144, 238, 144, 0) 80%) 50% 28% / 100% .2em,
        linear-gradient(to right, rgba(144, 238, 144, 0) 10%, rgba(144, 238, 144, 0.3) 30%, rgba(144, 238, 144, 0.3) 50%, rgba(144, 238, 144, 0) 70%) 50% 40% / 100% .2em, 
        linear-gradient(to right, rgba(144, 238, 144, 0) 30%, rgba(144, 238, 144, 0.3) 50%, rgba(144, 238, 144, 0.3) 70%, rgba(144, 238, 144, 0) 90%) 50% 50% / 100% .2em, 
        linear-gradient(to right, rgba(0, 128, 0, 0) 20%, rgba(0, 128, 0, 0.6) 40%, rgba(0, 128, 0, 0.6) 60%, rgba(0, 128, 0, 0) 80%) 50% 68% / 100% .2em;
}
</style>
```

<div class="ellipse">
    <div></div>
</div>
<style>
.ellipse{
    background-color: #f7f7f7;
    width:100%;
    height:200px;
    position: relative;
}
.ellipse > div {
    width: 220px;
    height: 60px;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-top: -30px;
    margin-left: -110px;
    border-radius: 2em;
    background-color: #3cb371;
    box-shadow: inset 0 -.7em 1em .4em #008000, 0 0 0 .1em #008000;
    background: 
        radial-gradient(circle at 50% 100%, #008000 40%, rgba(0, 128, 0, 0) 40.5%) 20% 7% / 2em 1em,
        radial-gradient(circle at 50% 100%, #008000 40%, rgba(0, 128, 0, 0) 40.5%) 80% 11% / 1.5em .75em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 30% 30% / 1em 1em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 38% 35% / .6em .6em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 15% 50% / 1em 1em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 78% 33% / .6em .6em, 
        radial-gradient(circle, #90ee90 50%, rgba(144, 238, 144, 0) 50.5%) 85% 40% / 1em 1em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 25% 60% / 1em 1em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 65% 50% / 1em 1em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 50% 70% / 1em 1em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 68% 65% / .6em .6em, 
        radial-gradient(circle, #008000 50%, rgba(0, 128, 0, 0) 50.5%) 75% 70% / 1em 1em, 
        radial-gradient(circle at 50% 0, #008000 40%, rgba(0, 128, 0, 0) 40.5%) 35% 93% / 1.5em .75em,
        linear-gradient(to right, rgba(144, 238, 144, 0) 20%, rgba(144, 238, 144, 0.6) 40%, rgba(144, 238, 144, 0.6) 60%, rgba(144, 238, 144, 0) 80%) 50% 28% / 100% .2em,
        linear-gradient(to right, rgba(144, 238, 144, 0) 10%, rgba(144, 238, 144, 0.3) 30%, rgba(144, 238, 144, 0.3) 50%, rgba(144, 238, 144, 0) 70%) 50% 40% / 100% .2em, 
        linear-gradient(to right, rgba(144, 238, 144, 0) 30%, rgba(144, 238, 144, 0.3) 50%, rgba(144, 238, 144, 0.3) 70%, rgba(144, 238, 144, 0) 90%) 50% 50% / 100% .2em, 
        linear-gradient(to right, rgba(0, 128, 0, 0) 20%, rgba(0, 128, 0, 0.6) 40%, rgba(0, 128, 0, 0.6) 60%, rgba(0, 128, 0, 0) 80%) 50% 68% / 100% .2em;
    background-repeat: no-repeat;
}
</style>


### 复杂的案列
绘制一个手提袋

#### 一、绘制袋身

```html
// 外层div只设置宽高和背景
<div id="rhyme">
    // 内层div绘制手提袋
    <div></div>
</div>
<style>
    /* 让内容居中显示 */
    #rhyme div {
        position: absolute;
        left: 50%;
        top: 50%;
    }
    #rhyme{
        background-color: #4169e1;
    }
    /* 上面内容后续就不在重复写了 */
     /* 设置袋身的宽高背景 */
    #rhyme div{
        width: 10em;
        height: 12em;
        margin-left: -5em;
        margin-top: -3.5em;
        background-color: #304355;
        background-repeat: no-repeat;
        background-size: 100% .1em;
        background-position: 0 1em;
        border-radius: .1em .1em .5em .5em;
        font-family: Helvetica, Arial, sans-serif;
        font-weight: bold;
        text-align: left;
        box-shadow: inset 0 .07em .1em #273645, inset 0 0 .3em .2em #273645;
    }

</style>
```

<div  id="rhyme1">
    <div></div>
</div>

<style>
    #rhyme1 div {
        position: absolute;
        left: 50%;
        top: 50%;
    }
    #rhyme1{
        background-color: #4169e1;
        width:100%;
        height:400px;
        position: relative;
    }
    #rhyme1 div{
        width: 10em;
        height: 12em;
        margin-left: -5em;
        margin-top: -3.5em;
        background-color: #304355;
        background-repeat: no-repeat;
        background-size: 100% .1em;
        background-position: 0 1em;
        border-radius: .1em .1em .5em .5em;
        font-family: Helvetica, Arial, sans-serif;
        font-weight: bold;
        text-align: left;
        box-shadow: inset 0 .07em .1em #273645, inset 0 0 .3em .2em #273645;
    }
</style>


#### 二、 绘制提手和袋身文字
```css
/* 把袋身中的文字也插入 */
#rhyme div:before {
    content: '-Barack Obama';
    font-size: 12px;
    width: 8.35em;
    height: 21.8em;
    left: 50%;
    margin-left: -4.175em;
    top: -8em;
    display: flex;
    justify-content: flex-end;
    align-items: flex-end;
    background-repeat: no-repeat;
    background-image: 
        linear-gradient(135deg, #18222b 40%, #212e3b 60%), 
        linear-gradient(-135deg, #18222b 40%, #212e3b 60%), 
        linear-gradient(to top, #212e3b, #304355 25%), 
        linear-gradient(to top, #212e3b, #304355 25%);
    background-size: 55% 1.2em, 55% 1.2em, 1.2em 8em, 1.2em 8em;
    background-position: 0 0, 100% 0, 1.4em 0, right 1.4em top;
    border-radius: 1.2em 1.2em 0 0;
    box-shadow: inset 1.2em 0 0 #304355, inset -1.2em 0 0 #304355;
    font-style: italic;
    color: white;
}

```

<div  id="rhyme2">
    <div></div>
</div>

<style>
    #rhyme2 div {
        position: absolute;
        left: 50%;
        top: 50%;
    }
    #rhyme2{
        background-color: #4169e1;
        width:100%;
        height:400px;
        position: relative;
    }
    #rhyme2 div{
        width: 10em;
        height: 12em;
        margin-left: -5em;
        margin-top: -3.5em;
        background-color: #304355;
        background-repeat: no-repeat;
        background-size: 100% .1em;
        background-position: 0 1em;
        border-radius: .1em .1em .5em .5em;
        font-family: Helvetica, Arial, sans-serif;
        font-weight: bold;
        text-align: left;
        box-shadow: inset 0 .07em .1em #273645, inset 0 0 .3em .2em #273645;
    }
    #rhyme2 div:before {
        position:absolute;
        content: '-Barack Obama';
        font-size: 12px;
        width: 8.35em;
        height: 21.8em;
        left: 50%;
        margin-left: -4.175em;
        top: -8em;
        display: flex;
        justify-content: flex-end;
        align-items: flex-end;
        background-repeat: no-repeat;
        background-image: linear-gradient(135deg, #18222b 40%, #212e3b 60%), linear-gradient(-135deg, #18222b 40%, #212e3b 60%), linear-gradient(to top, #212e3b, #304355 25%), linear-gradient(to top, #212e3b, #304355 25%);
        background-size: 55% 1.2em, 55% 1.2em, 1.2em 8em, 1.2em 8em;
        background-position: 0 0, 100% 0, 1.4em 0, right 1.4em top;
        border-radius: 1.2em 1.2em 0 0;
        box-shadow: inset 1.2em 0 0 #304355, inset -1.2em 0 0 #304355;
        font-style: italic;
        color: white;
    }
</style>

#### 三、绘制针线缝合纹路和袋身主题文字

```css
#rhyme div:after {
    position: absolute;
    font-size: 30px;
    content: 'Don’t moo. Vote.';
    box-sizing: border-box;
    width: 100%;
    height: 100%;
    padding: 1.2em 1em;
    background-repeat: no-repeat;
    background-image: 
        linear-gradient(#1e2934, #1e2934), 
        linear-gradient(#1e2934, #1e2934), 
        linear-gradient(45deg, transparent 45%, #1e2934 48%, #1e2934 52%, transparent 55%), 
        linear-gradient(-45deg, transparent 45%, #1e2934 48%, #1e2934 52%, transparent 55%), 
        linear-gradient(#1e2934, #1e2934), 
        linear-gradient(#1e2934, #1e2934), 
        linear-gradient(45deg, transparent 45%, #1e2934 48%, #1e2934 52%, transparent 55%), 
        linear-gradient(-45deg, transparent 45%, #1e2934 48%, #1e2934 52%, transparent 55%), 
        linear-gradient(#1e2934, #1e2934);
    background-size: .07em .4em, .07em .4em, .4em .4em, .4em .4em, .07em .4em, .07em .4em, .4em .4em, .4em .4em, 100% .07em;
    background-position: 1em 0, 1.4em 0, 1em 0, 1em 0, right 1em top, right 1.4em top, right 1em top, right 1em top, 0 .4em;
    border-radius: .06em .06em .3em .3em;
    color: white;
    text-shadow: .1em .1em 0 rgba(255, 255, 255, 0.2);
    line-height: 1.1;
}
```



<div  id="rhyme3">
    <div></div>
</div>

<style>
    #rhyme3 div {
        position: absolute;
        left: 50%;
        top: 50%;
    }
    #rhyme3{
        background-color: #4169e1;
        width:100%;
        height:400px;
        position: relative;
    }
    #rhyme3 div{
        width: 10em;
        height: 12em;
        margin-left: -5em;
        margin-top: -3.5em;
        background-color: #304355;
        background-repeat: no-repeat;
        background-size: 100% .1em;
        background-position: 0 1em;
        border-radius: .1em .1em .5em .5em;
        font-family: Helvetica, Arial, sans-serif;
        font-weight: bold;
        text-align: left;
        box-shadow: inset 0 .07em .1em #273645, inset 0 0 .3em .2em #273645;
    }
    #rhyme3 div:before {
        position:absolute;
        content: '-Barack Obama';
        font-size: 12px;
        width: 8.35em;
        height: 21.8em;
        left: 50%;
        margin-left: -4.175em;
        top: -8em;
        display: flex;
        justify-content: flex-end;
        align-items: flex-end;
        background-repeat: no-repeat;
        background-image: linear-gradient(135deg, #18222b 40%, #212e3b 60%), linear-gradient(-135deg, #18222b 40%, #212e3b 60%), linear-gradient(to top, #212e3b, #304355 25%), linear-gradient(to top, #212e3b, #304355 25%);
        background-size: 55% 1.2em, 55% 1.2em, 1.2em 8em, 1.2em 8em;
        background-position: 0 0, 100% 0, 1.4em 0, right 1.4em top;
        border-radius: 1.2em 1.2em 0 0;
        box-shadow: inset 1.2em 0 0 #304355, inset -1.2em 0 0 #304355;
        font-style: italic;
        color: white;
    }
    #rhyme3 div:after {
        position:absolute;
        font-size: 30px;
        content: 'Don’t moo. Vote.';
        box-sizing: border-box;
        width: 100%;
        height: 100%;
        padding: 1.2em 1em;
        background-repeat: no-repeat;
        background-image: linear-gradient(#1e2934, #1e2934), linear-gradient(#1e2934, #1e2934), linear-gradient(45deg, transparent 45%, #1e2934 48%, #1e2934 52%, transparent 55%), linear-gradient(-45deg, transparent 45%, #1e2934 48%, #1e2934 52%, transparent 55%), linear-gradient(#1e2934, #1e2934), linear-gradient(#1e2934, #1e2934), linear-gradient(45deg, transparent 45%, #1e2934 48%, #1e2934 52%, transparent 55%), linear-gradient(-45deg, transparent 45%, #1e2934 48%, #1e2934 52%, transparent 55%), linear-gradient(#1e2934, #1e2934);
        background-size: .07em .4em, .07em .4em, .4em .4em, .4em .4em, .07em .4em, .07em .4em, .4em .4em, .4em .4em, 100% .07em;
        background-position: 1em 0, 1.4em 0, 1em 0, 1em 0, right 1em top, right 1.4em top, right 1em top, right 1em top, 0 .4em;
        border-radius: .06em .06em .3em .3em;
        color: white;
        text-shadow: .1em .1em 0 rgba(255, 255, 255, 0.2);
        line-height: 1.1;
    }
</style>

## 三角形


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

## 其他技巧

### 磨砂玻璃效果 

<div class="yds">
    <div class="yds1">
        <div class="yds11">
            <h1 style="color:#CDDC39;">全国人民你最牛，骑着板凳上月球，天下数你最能吹，喝酒用缸不用杯。</h1>
            <h2 style="color:#FFC107;">全国人民你最牛，骑着板凳上月球，天下数你最能吹，喝酒用缸不用杯。</h2>
            <h3 style="color:#9E9E9E;">全国人民你最牛，骑着板凳上月球，天下数你最能吹，喝酒用缸不用杯。</h3>
            <button style="min-width: 100px;height: 50px;background: #F44336;border: 1px solid;">全国人民你最牛，骑着板凳上月球，天下数你最能吹，喝酒用缸不用杯。</button>
            <button style="min-width: 100px;height: 50px;background: #03A9F4;border: 1px solid;">全国人民你最牛，骑着板凳上月球，天下数你最能吹，喝酒用缸不用杯。</button>
            <button style="min-width: 100px;height: 50px;background: #009688;border: 1px solid;">全国人民你最牛，骑着板凳上月球，天下数你最能吹，喝酒用缸不用杯。</button>
            <hr style="border-bottom: 1px solid rgb(0, 0, 0);">
            <input />
            <div>全国人民你最牛，骑着板凳上月球，天下数你最能吹，喝酒用缸不用杯。</div>
            <hr style="border-bottom: 1px solid #000000;">
        </div>
        <div class="yds22">
    </div>
</div>
<style>
    .yds{
        position: relative;
        width:100%;
        height:200px;
    }
    .yds1{
        width:100%;
        height:200px;
        border:1px solid #ccc;
        overflow: auto;
    }
    .yds11{
        width: 100%;
        padding: 40px;
        word-wrap: break-word;
        overflow-wrap: break-word;
    }
    .yds22{
        width: 80%;
        height: 40%;
        border: 1px solid #ccc;
        position: absolute;
        top: 20%;
        left: 10%;
        background-image: radial-gradient(transparent 1px, #ffffff 1px);
        background-size: 4px 4px;
        backdrop-filter: saturate(50%) blur(4px);
    }
</style>