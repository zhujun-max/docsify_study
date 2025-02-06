
### 行，块，行内块元素都有哪些

**行内元素：**span、a、  
<span style="    font-size: 12px;
    line-height: 10px;
    color: #878787;">注意：行内元素设置margin的上下高度是无效的<br>padding的上下高度只会影响边框和背景</span>

**块级元素：**p、div、form、hr、h1~h6、

**行内块元素：**img、select、textarea、input、video、button



### flex布局

> 容器属性

1. flex-direction（主轴方向）  
    row（默认）：主轴为水平方向，起点在左端。  
    row-reverse：主轴为水平方向，起点在右端。   
    column：主轴为垂直方向，起点在上沿。  
    column-reverse：主轴为垂直方向，起点在下沿。   

2. flex-wrap（换行）  
    nowrap（默认）：不换行（设置的项目的宽度就失效了，强行在一行显示）。  
    wrap：换行。  
    wrap-reverse：换行，第一行在下方。  

3. flex-flow（方向 换行）  
    flex-direction和flex-wrap的简写。默认值为row nowrap。

4. justify-content（主轴对齐方式）  
    flex-start（默认）：左对齐。  
    flex-end：右对齐。  
    center：居中。  
    space-between：两端对齐，项目之间的间隔都相等。  
    space-around：每个项目的两侧间隔都相等，所以项目之间的间隔比边框大一倍。  

5. align-items（交叉轴对齐方式，上下高度对其）  
    flex-start：交叉轴的起点对齐，顶部对齐。  
    flex-end：交叉轴的终点对齐，底部对齐。  
    center：交叉轴的中点对齐。  
    baseline：项目的第一行文字的基线对齐。  
    stretch（默认）：如果项目未设置高度或设auto，将占满容器的高度。 

6. align-content（多轴对齐方式。如果项目只有一根轴线，该属性不起作用）   
    flex-start：交叉轴的起点对齐，顶部对齐。  
    flex-end：交叉轴的终点对齐，底部对齐。  
    center：交叉轴的中点对齐。  
    space-between：与交叉轴两端对齐，轴线之间的间隔平均布局。  
    space-around：每根轴线两侧的间隔都相等。项目之间的间隔比边框的间隔大一倍。  
    stretch（默认值）：轴线占满整个交叉轴。


> 项目属性

1. order（排列顺序，默认0）   
    项目的排列顺序，数值越小越靠前，默认为0。可负数

2. flex-grow（放大比列，默认0）  
    项目的放大比列，默认为0，如果存在剩余空间，也不放大。
    如果所有项目属性值都大于0并相同，则他们将等分剩余空间。

3. flex-shrink（缩小比列，默认1）  
    项目的缩小比列，默认为1。  
    属性为0时，将不会缩小，负值无效。  

4. flex-basis（项目占据固定大小）  
  定义有多余空间，项目占据的主轴空间大小，默认为auto（原本的大小）。  
  可以设置和宽高一样的属性，px，%，vh都可以用。  

5. flex（放大 缩小 大小三属性的缩写）  
  flex-grow，flex-shrink，flex-basis的简写，默认为0 1 auto，后两个可选。  

6. align-self（允许单个项目有不一样的对齐方式）   
    auto：继承父元素的align-items属性。  
    flex-start：交叉轴的起点对齐，顶部对齐。  
    flex-end：交叉轴的终点对齐，底部对齐。  
    center：交叉轴的中点对齐。  
    baseline：项目的第一行文字的基线对齐。  
    stretch（默认值）：如果项目未设置高度或设auto，将占满容器的高度。  

### Grid布局???



### BFC布局

其作用是使内部元素的布局不受外部元素影响。

**BFC的触发条件**
+ 根元素，也就是html、body根标签
+ position：fixed/absoluted
+ float属性值不是none的
+ overflow属性值不是visible的
+ display属性值：inline-block/table-cell/flex

**BFC的作用**
+ bfc内部元素的布局不受外部元素影响。
+ bfc区域不会出现margin重叠
+ bfc区域计算高度时候会自动计算浮动元素
+ bfc区域不会和浮动元素重合


### position有哪些属性

1. relative：相对定位；根据自身为基准点进行定位，不脱离文档流，只改变自身的位置，还是会占用原来的位置。(可以使用top、bottom、right、left)
2. absolute：绝对定位；根据有定位的父元素为基准进行定位，脱离文档流，不占用原来的位置。
3. fixed：固定定位；类似absolute，但不随滚动条的位置而改变。
4. sticky：粘性定位；它是 relative 和 fixed 的结合体，能够实线类似吸附的效果，当滚动页面时它的效果与 relative 相同，当要滚动到屏幕之外时则会自动变成 fixed 的效果。
5. static：默认值；默认布局（使用z-index无效）。

### css定位和层级
1. z-index只有设置了定位才能生效（设置static默认定位是无效的）
2. 层级一样的情况下，后者的元素会覆盖前者。
3. 标准 < 浮动 < 定位

<div class="levelRelationship">
    <div class="levelone">标准流</div>
    <div class="leveltwo">浮动</div>
    <div class="levelthree">定位</div>
</div>

<style>
.levelRelationship{
    width:200px;
    height:200px;
    position: relative;
}
.levelRelationship>div{
    color:#fff;
    width:100px;
    height:100px;
}
.levelRelationship>.levelone{
    background-color:red;
}
.levelRelationship>.leveltwo{
    background-color:green;
    float:left;
    margin-top: -60px;
    margin-left: 40px;
}
.levelRelationship>.levelthree{
    background-color:blue;
    position: absolute;
    top: 80px;
    left: 80px;
    z-index:2;
}
</style>



### 消除浮动

**产生原因：**  
1. 当父元素不给高度的时候；  
2. 子元素设置了float浮动属性；

**解决方案：**  
1. 在标签的最后位置添加一个div标签，设置`clear: both;` 
2. 给父元素添加overflow属性  
3. 让父级元素也浮动  
4. 给邻接元素添加`clear:both; ` 
5. 给父级设置after元素，设置  
   ```css
   .clearfix:after{
     content: "";
     display: block; 
     height: 0; 
     clear: both; 
     visibility: hidden;  
   }
   ```

### 伪类和伪元素的区别

伪类：特殊的class选择器，或是用来添加一些特殊效果。（只能使用单冒号）

伪元素：为选中的元素添加指定的内容。（可以使用双冒号）



<!-- 伪类：![image.png](./img/03.png) -->

| 伪类                    | 作用                                        |
| ------------------------| -----------------------------------------  |
| :active                 | 将样式添加到被激活的元素                     | 
| :focus                  | 将样式添加到被选中的元素                      | 
| :hover                  | 当鼠标悬浮在元素上方时，向元素添加样式         | 
| :link                   | 将特殊的样式添加到未被访问过的链接             | 
| :visited                | 将特殊的样式添加到被访问过的链接              | 
| :first-child            | 将特殊的样式添加到元素的第一个子元素           |
| :lang                   | 允许创作者来定义指定的元素中使用的语言         | 

<!-- 伪元素：![image.png](./img/04.png) -->
| 伪元素               | 作用                                        |
| ---------------------| -----------------------------------------  |
| :first-letter        | 将特殊的样式添加到文本的首字母                | 
| :first-line          | 将特殊的样式添加到文本的首行                  | 
| :before              | 在某元素之前插入某些内容                      | 
| :after               | 在某元素之后插入某些内容                      | 


### display:none;和visibility:hidden;的区别

`display:none;` 将元素的显示设为无，即在网页中不占任何的位置。能引发页面的reflow回流（重排）。

`visibility:hidden;` 仅仅是在视觉上看不见，空间位置仍然存在。好比`opacity:0;` 不引发页面回流。


### 重绘和回流

**回流：**引起DOM树结构变化，页面布局变化的行为叫回流,且回流一定伴随重绘。      
 <span style="    font-size: 12px;
    line-height: 10px;
    color: #878787;">回流也被称为重排。本质相近。回流：更侧重于元素位置和大小的重新计算。重排：更侧重于整个布局或页面的重新排列。</span>     

**重绘：**只是样式的变化，不会引起DOM树的变化，页面布局的行为叫重绘，且重绘不一定会伴随回流。


### CSS 优先级和权重值如何计算

+ !important。它会覆盖页面内任何位置定义的元素样式。（ie6支持上有些bug）。
+ 内联样式，如：style=“color:red;”，权值为`1000`.（该方法会造成css难以管理，所以不推荐使用）
+ ID选择器，如：#header，权值为`0100`.
+ 类、伪类、属性选择器, 如：.bar， 权值为`0010`.
+ 标签、伪元素选择器，如：div ::first-line 权值为`0001`.
+ 通配符，子选择器，相邻选择器等。如*，>,+, 权值为`0000`.
+ 继承的样式没有权值



<details> 
   <summary>权重四元组</summary>


**权重四元组是用于表示CSS选择器权重的四个数字组合，这四个数字分别代表了不同类型选择器的数量，从左到右级别依次降低。权重四元组的具体组成部分如下：**

**[a,b,c,d]**

**第一个数字（a位置）：**
代表内联样式的数量。（但实际上，内联样式通常不直接用这个四位数来表示，因为它的优先级是固定的，且非常高，可以覆盖其他所有样式规则。在权重计算时，内联样式通常被视为一个特殊的优先级，而不是作为权重四元组的一部分）

**第二个数字（b位置）：**
代表ID选择器的数量。

**第三个数字（c位置）：**
代表类、伪类、属性选择器的数量。

**第四个数字（d位置）：**
代表标签、伪元素选择器的数量。

!> **权重计算永不进位**

需要注意的是，权重四元组中的每个数字都是独立计算的，并且不会相互进位。也就是说，即使某个级别的选择器数量很多，也不会影响到其他级别选择器的权重值。

在CSS样式表中，当多个选择器作用于同一个元素时，浏览器会根据权重四元组来计算每个选择器的权重，并决定哪个样式规则应该被应用。权重越高的选择器，其对应的样式规则就越有可能被应用。

总的来说，权重四元组是CSS权重计算的基础，它帮助我们确定了不同选择器在CSS样式表中的优先级顺序。
</details> 


### 盒子模型是什么

**标准盒模型 ：** W3C标准的盒子模型（更常用）       
**怪异盒模型：**IE标准的盒子模型    
    
标准的盒子模型由：**content(区域内容大小) + padding(内边距) + border(边框) + margin(外边距)组成**  

#### 标准盒模型

设置：`box-sizing: content-box;`

设置宽高将限制`content`

**设置固定宽高后，更改padding和border都不会影响整体宽高**


<details> 
    <summary>垂直两个div外边距重叠问题</summary>

两个垂直方向的div，上面div设置了margin:10px。下面的div设置了margin:20px;那么两个div之间的距离按理说应该是10
+20=30px。

实际他们之间的距离是20px。为什么？

**这是因为浏览器上下放置两个块元素时，它们垂直方向的外边距会发生重叠，浏览器会把他们之间的外边距会折叠在一起，折叠后的外边距就是两个外边距中较大的那个外边距的大小。**

所以重新计算两个div垂直方向之间的距离为：

`max(margin-bottom(div.box1),margin-top(div.box2))=max(10px,20px)=20px`

</details>



<details> 
    <summary>父子嵌套div外边距重叠问题</summary>

如果一个元素嵌套在另外一个元素中，他们都有外边距，也会重叠吗？（父级外边距折叠塌陷问题）。
<div style="border: 1px solid;">
    <div style="width: 200px;height: 200px;margin: 10px;background:antiquewhite;">
        <div style="width: 100px;height: 100px;margin: 30px;background:aqua;"></div>
    </div>
</div>

**水平方向：**正常。
**垂直方向：**父级div和子级div外边距发生了重叠，**取二者中较大者**

**解决方法：**
+ 给父级1px的边框
+ 给父级1px内边距
+ 不用margin-top，改用父级内边距padding   
+ 给父元素设置overflow:hidden; （触发bfc）父元素会变成独立的空间
+ 将子元素转换为行内块元素

</details>

#### 怪异盒模型

设置： `box-sizing:border-box;`

设置宽高将限制`content + padding + border`




### 书写顺序

增加可读性和维护性。性能优化，避免覆盖和冲突。

1. 位置属性：`position、top、right、z-index、display、float`
2. 大小：`width、height、padding、margin`
3. 文字系列：`font、line-height、letter-spacing、color-text-align`
4. 背景：`background、border`
5. 其他：`animation、transition`
