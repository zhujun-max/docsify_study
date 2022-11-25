  <center><h1>web面试题</h1></center>

## CSS基础问题



### 行，块，行内块元素都有哪些

**行内元素：**span、a、

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
    space-around：每根轴线两侧的间隔都相等。所以，项目之间的间隔比边框的间隔大一倍。  
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



### BFC 自适应布局

bfc：其作用是使内部元素的布局不受外部元素影响。

**BFC的触发条件**

+ 根元素，也就是html根标签
+ position：fixed/absoluted
+ float属性值不是none的
+ overflow属性值不是visible的
+ display属性值：inline-display/table-cell/table-caption/flex/inline-flex;

**BFC的作用**

+ bfc内部元素的布局不受外部元素影响。
+ bfc区域不会出现margin重叠
+ bfc区域计算高度时候会自动计算浮动元素
+ bfc区域不会和浮动元素重合



###  css垂直居中

+ 方式1：绝对定位

  ```css
  porentElement{
      posotion:relative;
  }
  childElement{
      position:absolute;
      top:50%;
      left:50%;
      transform: translate(-50%,-50%);
  }
  ```

+ 方式2：flex布局

  ```css
  parentElement{
      display:flex;
      align-items: center;
      justify-content: center;
  }
  ```




### 左右固定，中间实现自适应

**1.float实现**

```html
<div>
    <div style="float: left;width: 200px;">left</div>
    <div style="margin: 0 200px;">middle</div>
    <div style="float: right;width: 200px;">right</div>
</div>
```

**2.flex实现**

```html
<div style="display:flex;">
    <div style="width: 200px;">left</div>
    <div style="flex:1;">middle</div>
    <div style="width: 200px;">right</div>
</div>
```



### position有哪些属性

1. absolute:绝对定位；脱离文档流的布局，遗留下来的空间由后面的元素填充。
2. relative：相对定位；不脱离文档流的布局，只改变自身的位置，在文档流原先的位置遗留空白区域。
3. fixed：固定定位；类似absolute，但不随滚动条的位置而改变。
4. static：默认值；默认布局。



### 消除浮动

**产生原因：**

​	当父元素不给高度的时候；

​	子元素设置了float浮动属性；

**解决方案：**

1. 在标签的最后位置添加一个div标签，设置clear: both;

2. 给父元素添加overflow属性

3. 让父级元素也浮动

4. 给邻接元素添加clear:both;

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




### 盒子模型是什么

盒子模型由四个部分组成： 

margin（外边距）， border（边框），padding（内边距），content（内容）

如果就想用设置宽高来当总体的宽高度 ，就设置一个box-sizing：border-box；



### CSS实现一个三角形

https://www.cnblogs.com/lidaying5/p/12605809.html

```css
#triangle-up {
    width: 0;
    height: 0;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 100px solid blue;
}
```

![img](./img/01.png)

```css
#triangle-topleft {
    width: 0;
    height: 0;
    border-top: 100px solid red;
    border-right: 100px solid transparent;
}
```

![img](./img/02.png)

## 常见面试题



### MVC是什么

mvc是model-view-controller的缩写。

主要目的是对代码解耦，把混合在一起的代码拆分为3个部分。

让html中不存在任何逻辑代码，没有javascript代码痕迹。

***

以原生HTML为例：

+ model：数据模型层

  > 早期前端：弱化的model，不关注Model层，数据都是从服务器下来，直接使用即可。
  >
  > 现在前端：使用webStorage，框架中的vuex，Redux等管理数据。
  >
  > 在TypeScript语言中，新增了数据类型声明特征，才让Model在前端变得尤为重要。

+ View：视图层

  > 书写普通的html，不掺杂任何js代码。
  >
  > 例如：<butt id='tedu'>Tedy</button>
  >
  > 注意：此按钮美誉偶onclick的事件写法。

+ Controller：控制层

  > 控制HTML的具体行为，具体为script代码范围。列入id=‘tedu’的按钮事件写法；
  >
  > ```javascript
  > var btn=docuent.getElementById("tedu");
  > btn.onclick=functon(){alret('123')}
  > ```
  >



###  MVVM是什么

MVVM就是Model-View-ViewModel的简写。他本质上就是MVC的改进版。MVVM就是将其中的view的状态和行为抽象化，让我们将视图UI和业务逻辑分开。

以vue为例：

+ Model：数据模型层

  > script部分的data属性，专门管理数据。

+ View：视图层

  > 即template中的代码，负责UI的构建。

+ ViewModel：视图模型层

  > new Vue({ })部分。自动管理数据和视图层。
  >
  > 重点是双向数据绑定功能，实现变化视图自动更新，视图变化，数据自动联动。

**解决了什么问题**

+ 开发者在代码中大量调用相同的DOM API，处理繁琐，操作冗余，使得代码难以维护。
+ 大量的DOM操作使页面渲染性能降低，加载速度变慢，影响用户体验。
+ 当Model频繁发生变化，开发者需要主动更新到View；当用户的操作导致Model发生变化，开发者同样需要将变化的数据同步到Model中，这样的工作不仅繁琐，而且很难维护复杂多变的数据状态。

> 其实，早期的jQuery的出现就是为了前端能更简洁的操作DOM而设计的，但它只解决了第一个问题，另外两个问题一直存在，MVVM的出现，完美的解决了以上三个问题。





###  Vue双向绑定原理

采用数据劫持 

结合发布者-订阅者模式的方式，

通过Object.defineProperty()来劫持各个属性的setter，getter，

在数据变化时发布消息给订阅者，

触发相应的监听回调。



具体步骤如下：

1. 首先，先要对observe的数据对象进行递归遍历，包括子属性对象的属性，都加上setter getter。这样的话，给这个对象的某个属性赋值，就会触发setter，那么就能监听到数据变化。（其实是通过Object.defineProperty（）实现监听数据变化的）

2. 然后，需要compile解析模板指令，将模板中的变量替换成数据，接着初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，订阅者收到通知，就会更新视图。

3. 接着，Watcher订阅者是Observer和Compile之间通信的桥梁，主要负责：

   ​	1）在自身实例化时，往属性订阅器（Dep）里面添加自己

   ​	2）自身必须有一个update()方法

   ​	3）待属性变动，dep.notice()通知时，就调用自身的updete()方法，并触发Compile中绑定的回调
   
4. 最后，viewmodel（vue实例对象）作为数据绑定的入口，整合Observer，Compile，Watcher三者，通过 Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起 Observer和Compile之间的通信桥梁，达到数据变化 (ViewModel)-》视图更新(view)；视图变化 (view)-》数据(ViewModel)变更的双向绑定效果。



###  Vuex是什么

Vuex是一个 **状态管理模式**。

它采用集中式存储管理，管理所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生改变。

使用场景：

+ 组件的状态共享：登录状态
+ 组件的数据共享：购物车的数据，登录的token。

5个核心属性：

+ state：数据存放
+ getters：相当于计算属性（一个变量被多次调用，就可以存放在getters中）调用后就会缓存起来，值发生了改变才会被重新计算。this.$store.getters.function
+ mutation：同步操作，修改数据，this.$store.commit('方法',值)
+ action：异步操作this.$store.dispatch(’方法‘,值)
+ modules：模块化



###  vue-router原理

https://blog.csdn.net/xiasohuai/article/details/81982821

vue-roter通过**hash、history、abstract**三种方式实现前端路由

更新视图但不重新请求页面是前端路由原理的核心之一

目前在浏览器环境中这一功能的实现主要有两种方式：

1. hash：利用URL中的hash，形式上会多个#

   #号的作用是加载URL中指定网页中的位置

   + hash虽然出现在url中，但不会被包括在http请求中，它是用来指导浏览器动作的，对服务器端完全无用，因为改变hash不会重新加载页面。

   + 每一次改变hash，都会在浏览器访问历史中增加一个记录。

     利用hash的以上特点，就可以来实现前端路由 "**更新视图不重新请求页面**“ 的功能。

2. history：html5中新增的方法，形式上比hash更好看

   history interoce是浏览器历史记录栈提供的接口，通过back()、forward()、go()等方法，我们可以读取浏览器历史记录栈的信息，进行各种跳转操作。

   从html5开始，history提供了2个新的方法：pushState()、replaceState()使得我们可以对浏览器历史记录栈进行修改

   这2个方法有个共同的特点：当调用他们修改浏览器历史栈后，虽然当前url改变了，但浏览器不会立即发送请求该url，这就是为单页应用前端路由，更新视图但不重新请求页面提供了基础

   > historty模式需要后端服务器进行 路由重写 处理，否则会报404错误

+ hash：使用URL hash值来做路由，默认传参

  + 改变hash并不会引起页面重载
  + HTTP请求不包括## ，所以使用hash不会影响到其他功能
  + 改变#会改变浏览器的访问历史
  + window.location.hash可以读取哈希值
  + JavaScript可以通过onhashchange监听到hash值的变化，这就意味着可以知道用户在浏览器手动改变了hash值

+ HTML5 history：依赖HTML5 History API 和服务器配置。

  ​	主要新增的两个api

  + pushState(状态对象，标题，URL)方法

    + 在浏览器历史记录栈中添加一个新的地址

  + replaceState(状态对象，标题，URL)方法

    + 替换当前的地址，不会去创建新的

      

+ abstract：支持所有JavaScript运行环境。如Node.js服务器



###  promise和await/async的区别

区别主要在于按顺序调用多个 异步函数 时的写法 和报错获取 

promise方法

promise是同步，then是异步

```javascript
ajax().then(fun1).then(fun2).then(fun3).then(fun4)
```

await/asycn方法

```javascript
async function  demo(){
    await res=aiax();
    await res=fun1(res);
    await res=fun2(res);
    await res=fun3(res);
    await res=fun4(res);
}
```

总结：

+  当遇到多个异步函数时
  + Promise方法需要很多.then，会导致代码不宜读且结构复杂
  + await/async方式让异步代码的格式于同步代码一样，更易读
+ 报错读取
  + Promise使用 .catch抓取
  + await/async使用try...catch...方式抓取错误

 

###  简述ES6使用到的新语句

1. let：块级作用域，不能重复声明，没有变量提升
2. const：常量；声明必须赋值，声明后的**基本数据类型无法被篡改**，引用类型可修改
3. 模板字符串
4. 解构赋值：let {name,age}={name:'dongdontg',age:33}
5. ... ：扩展运算符，代替arguments变量，接受函数的多余参数。function name(...age){}
6. 箭头函数：匿名函数，this永远指向其父作用域，不能用new创建，不能使用arguments
7. Promise：异步编程的一种方案，解决回调地狱
8. class 面向对象



###  v-if 和 v-show 的区别

区别

+ v-if
  + 通过删除DOM元素实现元素的隐藏
  + 惰性：只有条件为真时，才会加载元素到DOM树
+ v-show
  + 通过设置元素的css样式：display:none 实现元素的隐藏，不操作DOM
  + 非惰性：不管条件真与假，都会加载元素到DOM

所以

+ v-if 的开销比 v-show 更大
+ v-show 有更高的初始渲染消耗

使用场景

+ 一个元素频繁进行隐藏和显示，使用v-show更合适

+ 一个元素不频繁进行 隐藏和显示操作，使用v-if更合适

   列如：需要网络请求成功后才显示的内容



###  Vue的生命周期有哪些？使用场景？

**加载时**

+ beforeCreate：准备创建
  + data和methods都未创建，此处不能使用。用于插件开发中执行一些初始化任务
+ created：创建完毕
  + data和methods创建完毕，各种数据可以使用，常用于异步数据获取
+ beforeMount：开始挂载
  + 未执行渲染，更新，dom未创建
+ mounted：挂载完毕
  + 初始化结束，dom已创建，可以获取访问数据和dom元素。

**更新**

+ beforeUpdate：更新前
  + 更新前，用于获取更新前的各种状态
+ updated：更新完毕
  + 更新后，所有状态已是最新版

**销毁**

+ beforeDestroy：销毁前
  + 销毁前，用于一些定时器或订阅的取消
+ destroyed：销毁完毕
  + data和methods此处已消失，无法使用



### 组件通信方式

1、 props / emit 父传子，子传父

​	   缺点：多级嵌套组件

2、provide(破外特)与inject（鹰假可特）默认不是响应式

这对选项需要一起使用，以允许一个组件向其所有子孙后代注入一个依赖，无论层级有多深，都在其上下游关系成立的时间里始终生效。

​		缺点：子组件不能向祖先组件传递数据

```vue
// A组件 父级
<div>
      <h1>A 组件</h1>
      <ChildrenB />
</div>
  provide() {
    return {
      theme: this//方法一：提供祖先组件的实例
    };
  }

// F组件 子级或者孙级
<template functional>
  <div class="border2">
    <h3 :style="{ color: injections.theme.color }">F 组件</h3>
  </div>
</template>
<script>
export default {
  inject: {
    theme: {
      //函数式组件取值不一样
      default: () => ({})
    }
  }
};
</script>
```

3、$attrs （哦脆死）/ $listeners（你什哪丝）

 		能够实现子传祖

4、EventBus

​		类似vuex，实现全局通讯

```js
// 全局定义，将eventBus绑定到vue实例的原型上
Vue.prptptype.$EventBus=new Vue()

// 监听事件
this.$EventBus.$on('eventName',(param1,param2,...)=>{'函数'})

//触发事件
this.$EventBus.$emit('eventNmae', param1,param2,...)

// 移出监听事件
this.$eventBus.$off('eventName')
```

5、ref   $parent $children

​		缺点：1. 不能跨级访问

​				    2. 不能直接修改父组件的元素（可以通过给父组件传递事件修改）

```js
https://www.jianshu.com/p/e0d0125f8dd9
```



###  git常用命令

+ 本地仓库
  + 初始化：git init
  + 暂存：git add 文件名 或 get add .
  + 提交版本：git commit -m ’版本描述‘
  + 分支：git branch
  + 合并：git merge

+ 远程仓库
  + 克隆：git clone 远程仓库地址
  + 刷新：git fetch
  + 标签：git tag -a v0.12.1 -m ‘更新了什么’
  + 更新：git pull
  + 上传：git push 



###  什么是单页面应用

单页应用的全称是 Single Page Application，简称 SPA

通过路由的变更，局部切换网页内容，取代整个页面的刷新操作

三大框架均采用单页面应用模式

+ 优点
  1. 用户操作体验好，用户不用刷新页面。
  2. 局部更新，对服务器压力小
  3. 良好的前后端分离，后端不用在负责页面渲染和输出工作
+ 缺点
  1. 首次加载耗时长，速度慢
     1. 去掉编译后的map文件，map文件是帮助线上调试，查看样式，通常不生成map文件。
     2. vue-router路由懒加载 component: () => import( "@/index.vue")。（懒加载的文件会单独生成一个js文件，非懒加载的文件会统一生成一个app.js）
     3. 使用CDN减小代码体积加快请求速度
     4. 文件按需加载
  2. SEO不友好，需要采用prender服务进行完善



### vue权限管理

1、接口的访问权限一般传递token由后端判断返回状态码（一般由后端验证）

​	如果判断权限不够，直接弹出提示。跳转致登录页面或404页面。

2、页面的显示权限

​	原因：不同的用户有不同的权限，能访问的页面是不一样的。

​	解决：动态生成路由，利用vue-router的addRoutes方法可以动态添加路由





### 闭包

闭包函数：声明一个函数中的函数，叫做闭包函数

闭包：内层函数引用的外层函数作用域对对象，导致外层函数的作用域对象在调用后无法释放

```javascript
function funA(){
    var a=10;//funA的活动对象之中
    return funtion(){//匿名函数的活动对象
        console.log(a)
    }
}
var b=funA()
b()//10
```

闭包的使用场景

+ 读取函数内部的变量
+ 父函数中的变量始终保持在内存中存活，不会因为函数执行结束而消失

优点

+ 函数中的变量长期存在
+ 避免全局变量污染
+ 变量成为私有成员属性的存在

缺点

常驻内存会增大内存的使用量 使用不当会造成内存泄漏



###  跨域问题

原因：浏览器同源策略

浏览器从一个域名的网页去请求另一个域名的资源时，域名，端口，协议任一不同，都是跨域

常见的解决方案有3种：

+ cors

  + 由服务器解决，添加cors功能模块
  + 前端：无操作

+ jsonp：利用script脚本的src不受同源策略限制的特点（只能使用get）

  + 服务器：返回特定的jsonp格式数据

  + 前端：发送特定的jsonp格式数据到服务器

    ```javascript
        <div id='divCustomers'></div>
        <script>
        function callbackFunction(result,methodName){
            var html='<ul>';
            for(var i = 0; i < result.length; i++){
            html += '<li>' + result[i] + '</li>';
          }
          html += '</ul>';
        document.getElementById('divCustomers').innerHTML = html;
        }
        </script>
        <script type="text/javascript"
        src="https://www.runoob.com/try/ajax/jsonp.php?
        jsoncallback=callbackFunction">
        </script>
    
    ```

+ 代理proxy

  + vue、angualr都提供固定的方式设定代理

    ```javascript
    //vue-cli3.0里面的vue.config.js做配置
    devServer:{
        proxy:{
            '/rng': { //这里最好有一个 /
    		target: 'http://45.105.124.130:8081', // 后台接口域名
    	 	ws: true, //如果要代理 websockets，配置这个参数
     		secure: false, // 如果是https接口，需要配置这个参数
     		changeOrigin: true, //是否跨域
     		pathRewrite:{
     		'^/rng':''
     		}
          }
       }
    }
    ```

更多的方式：

+ html5新增的postMessage特性
+ websockwt方式
+ location.hash + iframe 
+ window.name + iframe 
+ document.domain + iframe





###  网络性能优化

+ 网络传输性能优化

  + 浏览器缓存
  + 资源打包压缩（js/html/css压缩，服务器Gzip压缩）
  + 图片资源优化 （webp，精灵图，字体图标）
  + 使用CDN
+ 页面渲染优化

  + css属性读写分离（最好不用js操作样式）
  + 通过切换class或者style去批量操作样式
  + 将没用的元素设置为不可见：visibility：heiden
  + 压缩dom深度，少用dom，多用伪元素
  + 图片指定大小，或者脱离文本流
+ js阻塞性能
  + 注意作用域的数量，访问作用域外的变量都会循环作用域链
  + 避免全局查找
  + 选择正确的方式，优化循环
  + 最小化语句
+ 负载均衡
  + nginx搭建反向代理



  ### vue路由守卫

### 完整的导航解析流程
>
>  	1.导航被触发。
>  	2.在失活的组件里调用 beforeRouteLeave 守卫。
>  	3.调用全局的 beforeEach 守卫。
>  	4.在重用的组件里调用 beforeRouteUpdate 守卫 (2.2+)。
>  	5.在路由配置里调用 beforeEnter。
>  	6.解析异步路由组件。
>  	7.在被激活的组件里调用 beforeRouteEnter。
>  	8.调用全局的 beforeResolve 守卫 (2.5+)。
>  	9.导航被确认。
>  	10.调用全局的 afterEach 钩子。
>  	11.触发 DOM 更新。
>  	12.调用 beforeRouteEnter 守卫中传给 next 的回调函数，创建好的组件实例会作为回调函数的参数传入。

总结：

路由守卫以一共有三种，全局路由守卫，组件内路由守卫，独享守卫。



+ 全局路由守卫 

  ```javascript
  //全局前置守卫                        
  router.beforeEach((to,from,next)=>{
      // 所有的路由都会走这个函数
      // 用于权限判断
  })
  
  //全局解析守卫
  router.beforeResolve((to,from,next)=>{
      // 和前置守卫一样，区别是等组件内守卫和异步组件执行完后，解析守卫才会被调用
  })
  
  //全局后置钩子
  router.afterEach((to.from)=>{
  	// 不接受next函数，也不会改变导航本身
  })
  ```

  

+ 路由独享守卫

  ```javascript
  const router = new VueRouter({
    routes: [
      {
        path: '/foo',
        component: Foo,
        beforeEnter: (to, from, next) => {
          // 直接在路由中配置，和beforeEach写法一样
        }
      }
    ]
  })
  ```

+ 组件内的守卫

  ```javascript
    beforeRouteEnter(to, from, next) {
      // 在渲染该组件的对应路由被 confirm 前调用
      // 不！能！获取组件实例 `this`
      // 因为当守卫执行前，组件实例还没被创建
    },
    beforeRouteUpdate(to, from, next) {
      // 在当前路由改变，但是该组件被复用时调用
      // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
      // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
      // 可以访问组件实例 `this`
    },
    beforeRouteLeave(to, from, next) {
      // 导航离开该组件的对应路由时调用
      // 可以访问组件实例 `this`
    }
  ```

  



### get和post的区别

+ **get在浏览器回退时是无害的，而post会再次提交请求**
+ get产生的url地址可以被Bookmark，而post不可以
+ get请求会被浏览器主动cache，而post不会，除非手动设置
+ get请求只能进行url编码，而post支持多种编码方式
+ **get请求参数会被完整保留在浏览器历史记录里，而post中的参数不会被保留**
+ **get请求在url中传送的参数时有长度限制的，而post没有**
+ 对参数的数据类型，get只接受ASCII字符，而post没有限制
+ get比post更不安全，因为参数直接暴露在url中，所以不能用来传递敏感信息
+ **get参数通过url传递，post放在Request body中**



### 数组操作函数

| 对象                     | 作用                                               | 返回值                   | 改变原数组 |
| ------------------------ | -------------------------------------------------- | ------------------------ | ---------- |
| push()                   | 向数组的末尾添加一个或多个元素                     | 返回新数组的长度         | 是         |
| pop()                    | 删除数组的最后一个元素                             | 返回删除的值             | 是         |
| unshift()                | 数组的头部添加一个或多个元素                       | 返回新数组的长度     | 是         |
| shift()                  | 删除数组的第一个元素                               | 返回删除的值             | 是         |
| reverse()                | 颠倒数组中的元素顺序                               | 返回颠倒后的值           | 是         |
| sort(a,b)                | 对数组元素进行排序（会先调用toString方法，然后按照字符串序列排序。也可以自定义排序） | 返回排序后的值           | 是         |
| forEach(item,index,arr) | 对所有元素执行函数，常用来遍历元素 | 无 | 是 |
| splice(start, end,value) | 可以删除，插入，替换 | 返回被替换/删除/插入的值 | 是 |
|isArray()					|用于检测是否为数组|返回true，false|否|
|toString()		|把元素转换为字符串，默认以逗号分割		|返回字符串|否|
|every(item,index,arr)	|对所有元素执行函数，全部都为true，返回true	|返回true，false|否|
|some()	|对所有元素执行函数，有一个为true，返回true	|返回true，false|否|
|filter(item,index,arr)	|对所有元素执行函数(自定义函数)	|返回满足条件的值|否|
|map(item,index,arr)	|对所有元素执行函数	|返回自定义函数结果|否|
| concat()                 | 拼接两个或多个数组                               | 返回合并的值             | 否         |
| join()                   | 把元素转成字符串，使用指定符号分割                 | 返回分割后的字符串        | 否         |
| slice(start, end)        | 截取元素                                           | 返回截取的值             | 否         |
| indexOf(x, start)        | 查找元素第一次出现的位置                           | 返回下标，没找到返回-1   | 否         |
| lastIndexOf(x,start)  | 查找元素最后一次出现的位置                         | 返回下标，没找到返回-1   | 否         |



### 循环的方式

for：不能遍历对象。

for in:只能遍历对象。

for of:不能遍历对象，同for循环一样。

map:对数组进行操作，返回一个新数组。(不会对空数组进行检测)。

forEach：对数组的操作会改变原数组。不应过度滥用。

filter：根据条件过滤数组中的某些值，最后返回布尔值。

reduce：返回结果为单个值（求和，找最大值。返回内容）

find：找到符合条件的项目并打算之后使用该项目（返回新内容）

some：检查是否符合条件，只要有一个条件符合，就返回true。（返回布尔值）

every：检查是否符合条件，所有项目都符合条件，才会返回true。（返回布尔值）

```javascript
//forEach
//需要迭代数组以执行特定操作（不返回参数）
const items=[1,2,3,4,5]
items.forEach(item=>console.log(item))

//filter
//根据条件过滤数组，在每次迭代中返回一个布尔值，否则js会强制转换为布尔（返回过滤后的新数组）
const evenValue = items.filter(currentValue => {
   return currentValue % 2 == 0 
})

//map
//将数组转为另一个数组（返回新数组）
const result=items.map(item=>{
    return nitem * 2
})

//reduce
//从数组中进行操作，返回结果为单个值。必须求和，求最大。（返回新结果）
const sum = items.reduce((accumulator, currentValue) => {
   return accumulator += currentValue
}, 0)

//find
//找到符合条件的项目（返回找到的结果,没有找到返回undefined）
const item = items.find(item => item === 3)

//some
//查找是否有符合条件的值（返回布尔值）
const item = items.some(item => item === 3)

//every
//匹配所有项目，全部为true，返回true（返回布尔值）
const item = items.every(item => item >= 20)


some()遍历每一项，一项返回true，则返回true。因此当 some 内部返回  true 时，跳出整个循环。
every()遍历每一项，全部true,则返回true。因此当 every 内部返回 false 时，跳出整个循环。
map()遍历每一项，返回一个新的数组，每个元素为调用函数处理后的值，return false 无法终止循环。
forEach()没有返回值，对数组中的每一项运行给定函数，参数都是 function 类型。return false 无法终止循环。
for()遍历数组，且通过 return false 或 break 终止循环。
```




### 前端的存储方式

localStorage：没有时间限制，永久存储，永不失效，除非手动删除，每个域名只有5兆（键也占空间），使用windown.localStorage可以检测，同域名多窗口共享。(IE只有3兆，其他的是5兆)

sessionstorage：使用方法和localStrage一样，区别在于sessionStorage浏览器关闭后即被删除。

IndexedDB：浏览器数据库，大于250兆，手动更新，
web sql: 页面刷新就丢失(不常用，基本要废弃)

token：把你要存储的用户信息加上算法，加上自己知道的密钥，做成一个签名，就形成一个token，别人不知道密钥，就无法伪造。

cookie：在客户端保存用户信息，保存的是String类型，cookie可以保存在客户端，保存不重要的信息，只能存4k。会携带在请求头中，而每次发送请求都会传输，浪费宽带。

session：在服务端保存用户信息，保存的是Object类型，会话结束而销毁，保存重要信息。



###  v-if和v-for的优先级

当v-if与v-for一起使用时，v-for具有比v-if更高的优先级，这意味这v-if将分别重复运行于每个v-for循环中

解决方案：

1. 放在计算属性遍历。（官方建议，还能兼容vue3）
2. 在外层加一个template标签，将v-for放在template标签之中。

vue内部把v-if的代码封装成一个匿名函数，传递给了v-for，而v-for最后实现时，再来执行v-if。



### vue中的methods,watch和computed区别

https://blog.csdn.net/ligang2585116/article/details/94590314

**计算属性computed** 

> 理论上，computed所有实现可以使用methods完全替换

1. 支持缓存，只有依赖数据发生改变，才会重现计算
2. 不支持异步，当computed内有异步操作时无效，无法监听数据的变化
3. 当页面中有某些数据依赖其他数据进行变动的时候，可以使用计算属性。
6. 监听数据不用在data中声明。

**侦听属性watch**

1. 不支持缓存，数据变会直接触发相应的操作；
2. watch支持异步。
3. 监听的函数接受两个参数，第一个参数是最新的值，第二个参数是输入之前的值；
4. 当一个属性发生变化时，需要执行对应的操作，一对多；
5.  监听数据必须是data中声明过或者父组件传递过来的props中的数据，当数据变化时，触发其他操作，函数有两个参数



### 离线存储哪些方式，各自适应的环境有哪些

localStorage：键值对的方式存储，永久存储，永不失效，必须手动删除，每个域名5M，不安全。

sessionStorage数据在浏览器关闭后自动删除，5M；

cookies：缺点是请求头带着数据，4k；

**Application Cache：**

实际开发中，主要是使用Application Cache和LocalStorage技术，它们来自HTML5技术。

（1）Application Cache：通常用于静态资源（静态页面）的缓存。
（2）LocalStorage：通常用于AJAX请求缓存，存储非关键性AJAX数据。

当页面有些元素它们是不变的，你可以使用Application Cache技术离线缓存掉，每次访问这些缓存过的元素就不需要再请求服务器了，当有些东西经常变，那就让它们每次请求服务器吧



### DOM事件流，完整的过程

**1.什么是DOM事件流：**

事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流。

专业解读：
DOM(文档对象模型)结构是一个树型结构，当一个HTML元素产生一个事件时，该事件会在元素结点与根结点之间的路径传播，路径所经过的节点都会收到该事件，这个传播过程可称为DOM事件流。

**2.DOM事件流的分类？分别是什么含义？**

DOM事件同时支持两种事件模型：捕获型事件和冒泡型事件流。

**冒泡事件流：**从下向上，body》html》document》window

注意：addEventListener(type,listener, useCapture)，useCapture默认为false，只能冒泡。改为true，只能捕获

**捕获型事件流：**从上而下，window》document》html》body》某个具体的元素

capature捕获，bubble冒泡。

**3.DOM事件流的三个阶段？**

1. 事件捕获阶段
2. 处于目标阶段
3. 事件冒泡阶段



**4.事件委托和事件代理？**

事件委托：也可以成为事件代理，也就是将原本绑定在子元素身上的事件委托给父元素。让父元素去监听事件。其原理是利用事件冒泡。	

一个事件触发后，会在子元素之间传播，或者传播分为3个阶段：

1. 事件捕获阶段：从window对象一次向下传播，到达目标阶段，即为捕获阶段。捕获阶段不会响应任何事件。
2. 处于目标阶段：在目标节点触发事件，即为目标阶段。
3. 事件冒泡阶段：从目标阶段依次向上传播，到达window对象，即为冒泡阶段。

事件委托的优点：可以减少事件的注册，节省内存占用。也可以实现当新增对象时无需再次对其绑定事件。

事件委托口语化描述：有两个组件，子组件和父组件，子组件还不存在，将来再创建，这时想给子组件设置事件，而子组件此时不存在，无法设置事件，怎么办呢？子组件就委托父组件元素帮他设置事件，我们称事件委托，这是站在子组件的角度考虑问题时叫事件委托。站在父组件的角度考虑问题，父组件代理了子组件给子组件绑定事件，称事件代理。所以事件委托和事件代理其实是一回事，只是站的角度不同而已。

**5.阻止事件传播**

e.stopPropagation()冒泡机制下，阻止事件的进一步往上冒泡。捕获机制下，阻止事件的进一步向下捕获。

e.cancelBubble 是e.stopPropagation() 的曾用名，也可以阻止冒泡和捕获
e.cancelBubble = true;



### 语义化

简单理解：根据内容的结构化，选择合适的标签，便于发者阅读和写出更加优化的代码。

优点：提升可访问性；

​			SEO；

​			结构清晰，利于维护；

语义化标签：title，h1~h6，header，nav，main，section，aside，footer，strong，em。



### js基础数据类型和引用类型区别，怎么判断

基本数据类型：Number、String 、Boolean、Null、Undefined、Symbol（ES6）、BigInt（ES10）。

引用类型：Object（Object，Array，Function，Date，Math，RegExp）。

*基本数据类型指的是简单的数据段，引用数据类型指的是有多个值构成的对象。*



**怎么判断：**

**typeof ：**不能区分object array null，返回值都是object。

**Object.prototype.toString.apply(x)：**

**constructor**，原型对象，unll和undefined无原型对象，所以判断不了

**instanceof **  可以正确判断引用类型，基础数据类型不能判断



### js作用域，作用域链是什么

**1. 什么是作用域:**

​     (1). 作用: 一个变量的可用范围

​     (2). 本质: 一个保存变量的对象

**为什么: 为了避免不同范围内的数据之间互相干扰！**

**包括: 2级:**

   *(1). 全局作用域: window对象*

​     a. 专门保存所有全局变量的作用域

​     b. 优点: 随处可用，可反复使用！

​     c. 缺点: 极易被污染

   *(2). 函数作用域 ?对象*

​     a. 专门保存仅函数内可用的局部变量的作用域

​     b. 优点: 因为仅函数内可用，所以不会被污染

​     c. 缺点: 不可重用！



**2.作用域链**

​     (1). 什么是: 由多级作用域串联形成的链式结构

​     (2). 每个函数在创建时，就有了自己的作用域链。普通函数作用域链里包含2个格:

​          离自己近的格，暂时为空，调用函数时，用来临时引用函数作用域对象

​          离自己远的格，始终保存着全局作用域对象window

​     (3). 保存着一个函数可用的所有变量

​     (4). 控制着变量的使用顺序: 先局部，局部没有，才全局！



### 原型与原型链

1. 为所有子对象保存共有方法的对象，成为原型对象。

2. 一个类型中，prototypr和_ _propo_ _其实指向的是同一个原型对象。

   1. prototypr属于构造函数对象，是站在和原型对象平级的位置，查找构造.prototypr.
   2. _ _peopo_ _属于每个子对象，是站在子级角度，称呼父对象。

   **访问原型对象：**构造函数.prorotypr

   **访问父对象：**子对象._ _propo_ _

![img](https://s1.ax1x.com/2022/03/29/q6JFq1.png)

```javascript
function Student(sname,sage){
  this.sname=sname;
  this.sage=sage;
}
Student.prototype.className="初一2班"
var lilei=new Student("Li Lei",11);
var hmm=new Student("Han Meimei",12);
console.log(lilei);
console.log(hmm);
//获取lilei的sname和className
console.log(lilei.sname,lilei.className)

console.log(lilei.className, hmm.className)
//修改className
//正确: 
Student.prototype.className="初二2班"
console.log(lilei.className, hmm.className)
//错误: 
lilei.className="六年级2班"
console.log(lilei.className, hmm.className);
//过了一年又升一级
Student.prototype.className="初三2班"
console.log(lilei.className, hmm.className)
```



### es6解构赋值使用场景

1、数组解构赋值

```js
// 解构
const colors = [ 'red', 'green', 'blue' ];
const [ firstColor, secondColor ] = colors;
console.log(firstColor); // "red"
console.log(secondColor); // "green"

// 直接省略元素，只为感兴趣的元素提供变量名
const [ , , thirdColor ] = colors;

// 解构赋值
firstColor = "black",
secondColor = "purple";
[ firstColor, secondColor ] = colors;

// 变量交换
let a = 1,
let b = 2;
[ a, b ] = [ b, a ];

// 默认值
const [ firstColor, secondColor = "green" ] = colors;

// 嵌套数组解构
const colors = [ "red", [ "green", "lightgreen" ], "blue" ];
// 随后
const [ firstColor, [ secondColor ] ] = colors;
console.log(firstColor); // "red"
console.log(secondColor); // "green"

// 不定元素
const [ firstColor, ...restColors ] = colors;
```

2、对象的解构赋值

  ``` js
  // 解构
    const info = {
        name: 'cao yuan',
        age: 666
    };
    const { name, age } = info;
    console.log(name); // "cao yuan"
    console.log(age); // 666

    // 解构赋值
    let name = 'hero', age = 18;
    ({ name, age, sex='man' } = info);

    // 默认值
    let { name, age, sex = 'man' } = info;

    // 为非同名局部变量赋值
    let { name: myName, age: myAge } = info;

	// 嵌套对象解构
	const info = {
        name: 'cao yuan',
        age: 666,
        child: {
            cInfo: {
                name: 'cao yuan child',
                age: 3,
            }
        }
    };
    let { child: { cInfo } } = info;
    console.log(cInfo.name); // "cao yuan child"
    console.log(cInfo.age); // 3

    /* 
    *1. 一定要用一对小括号包裹解构赋值语句，JS引擎将一对开放的花括号视为一个代码块。语法规定，代码块语句不允许出现在赋值语句左侧，添加小括号后可以将块语句转化为一个表达式，从而实现整个解构赋值过程
    *
    * 2. 解构赋值表达式(也就是等号（=）右侧的表达式)如果为null或undefined会导致程序抛出错误。也就是说，任何尝试读取null或undefined的属性的行为都会触发运行时错误
    * 
    * 3. 使用解构赋值表达式时，如果指定的局部变量名称在对象中不存在，那么这个局部变量会被赋值为undefined
    * 4. 为变量设置了默认值，只有当有该属性或者该属性值为undefined时该值才生效。
    */ 
  ```
3、字符串解构赋值

```js
// 字符串也可以解构赋值。这是因为，字符串被转换成了一个类数组的对象
const [a, b, c, d, e] = 'hello';

// 类数组的对象都有一个`length`属性，因此还可以对这个属性解构赋值
const { length } = 'hello';
console.log(length); // 5
```

4、数值与布尔解构赋值

```js
// 解构赋值时，如果等号右边是数值和布尔值，则会先转为对象
const { toString: s1 } = 123;
console.log(s1 === Number.prototype.toString); // true
const { toString: s2 } = true;
console.log(s2 === Boolean.prototype.toString); // true
// 解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错
const { prop: x } = undefined; // TypeError
const { prop: y } = null; // TypeError
```

5、 传参中的解构运用

```js
// 未使用解构
function setCookie(name, value, options) {
    options = options || {};
    let secure = options.secure,
        path = options.path,
        domain = options.domain,
        expires = options.expires;
}
// 解构
function setCookie(name, value, { secure, path, domain, expires }) {
// 设置 cookie 的代码
}

```

### 箭头函数的特点

箭头函数是匿名函数.
1.不能作为构造函数，不能使用new

```javascript
let foo=()=>{

}
var newFoo=new foo()//foo is not a construcotr
```

2.不能使用argumetns,取而代之用rest参数...解决

```javascript
let C = (...c) => {
  console.log(c);
}
C(1,2,3,3)
```

3.this永远指向其父级的作用域

​	箭头函数的this永远指向上级的this，call、apply、bind也无法改变

4.箭头函数没有原型对象





### 什么是虚拟dom，有什么好处

虚拟dom就是用来模拟DOM结构的一个js对象。

**减少对真实DOM的操作**

​	在vue，react技术出现之前，我们要改变页面展示的内容只能通过遍历查询dom树的方式找到需要修改的dom然后修改样式行为或者结构，来达到更新视图的目的。这种方式相当消耗计算资源，因为每次查询dom几乎都需要遍历整颗dom树，如果建立一个与dom树对应的虚拟dom对象（js对象），以对象嵌套的方式来表示dom树，那么每次dom树的更改就变成了js对象的属性的更改，这样一来就能查找js对象属性变化要比查询dom树的性能开销要小。

**vue的方式**

vue采用的是虚拟dom

通过重写setter，getter。

实现观察者监听data属性的变化。

生成新的虚拟dom

通过函数创建真实的dom

替换dom树上对应的旧dom。



**缺点**

无法进行极致优化：虽然虚拟DOM+合理的优化，足以应对绝大部分的性能需求，但在一些性能要求极高的应用中虚拟DOM无法进行针对性的极致优化。首次渲染大量DOM时，由于多了一层虚拟DOM的计算，会比innerHTML慢。



### 多维数组的扁平化

var arr = [[1, 2, 8, [6, 7]], 3, [3, 6, 9], 4]

**1. 递归**

```javascript
function getNewArr(arr){
    // 定义新数组用于存储所有元素
    var newArr=[];
    //遍历原数组中的每个元素
    for(var i=0;i<arr.length;i++){
        // 判断当前元素是否为数组
        if(Array.isArray(arr[i])){
            // 若当前元素为数组时，调用函数本身继续判断，通过concat方法连接函数返回的数组
            newArr=newArr.concat(getNewArr(arr[i]))
        }else{
            // 若不是数组直接将当前元素追加到新数组的末尾
            newArr.push(arr[i])
		}
    }
    // 循环结束将新数组返回
    return newArr
}
```

**2. 递归**

```javascript
var newArr=[]
function getNew(arr,newArr){
    // 遍历原始数组中的每一项
    for(var i=0;i<arr.length;i++){
        // 判断数组中的当前元素是否为数组
        if(Array.isArray(arr[i])){
            // 是数组时继续调用函数进行判断
            getNewArr(arr[i],newArr)
        }else{
            // 否则将当前元素追加到新数组中
            newArr.push(arr[i])
        }
    }
```

**3. toString、split和map结合使用对数组进行扁平化；该方法有局限性，必须都是数字，因为toSting会将数组中的元素转为字符串。**

```javascript
function getNewArr(arr){
    var newArr=arr.toString().split(',').map(function(item){
        // 使用+ 号将当前元素转为数字
        return +item
    })
    return newArr
}
```

**4.通过ES6中的...运算符**

```javascript
function getNewArr(arr){
    // 循环数组中的元素判断元素是否为数组
    while(arr.some(item=>Array.isArray(item))){
        // 解构数组
          arr=[].concat(...arr)
          }
    return arr
}
```

**5.正则**

```javascript
//改良正则
const res= JSON.parse('[' + JSON.stringify(arr).replace(/\[|\]/g, '') + ']');
```

**6. 使用reduce**

```javascript
const flatten=arr=>{
    return arr.reduce((pre,cur)=>{
        return pre.concat(Array.isArray(cur)?flatten(cur):cur);
    },[])
}
const res=flatten(arr)
```

**7. flat()**

```javascript
const res=arr.flat(Infinity)
// 会默认移除空内容，
```



### 解决首屏加载慢

单页面应用首次加载的文件较多，导致首屏渲染速度很慢。

安装webpack-bundle-analyzer插件，通过这个插件，可以看出打包文件的大小

**1. 路由懒加载**

**2. 压缩代码并移除console**

**3. 使用cdn，引用第三方库，静态资源oss减小服务器压力**

**4. 开启gzip**

**5. 去掉编译文件的中的map文件**

​	这些文件主要是帮助我们线上调试代码，查看样式。所以为了避免部署包过大，通常不生成这些文件。

​	在config/index.js文件中将productionSourceMap的值设置为false。





### 插槽slot，有几种方法

主要分三种，默认插槽、具名插槽、作用域插槽

**默认插槽**

```html
// 父组件
<children>
    <p>我会显示</p>
</children>

// 子组件
<div>
    <solt>我是默认信息</solt>
</div>
```

**具名插槽**

```html
// 父组件
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <template v-slot:default>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </template>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>

// 子组件
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```

**作用域插槽**

在template中写的变量是无法访问到父组件的，需要通过v-slot传值的方式，也叫作用域插槽

```html
// 父组件
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>

// 子组件
<span>
  <slot>{{ user.lastName }}</slot>
</span>
```



### vue-router 如何做历史返回提示

获取vue-router的上一个页面是否存在或者是否为自己需要返回的地址，可以使用vue-router的声明周期函数

+ 使用全局函数beforeEach，直接来获取form.path（即为对应的上一次地址的路由path内容）
+ 使用组件内共享函数beforeEnter，直接来获取form.path
+ 使用组件内函数，beforeRouteEnter，直接来获取form.path



###  防抖节流

防抖：事件连续触发，只执行最后一次。

```js
const input = document.querySelector('#input');
let timer = null;
input.addEventListener('keyup', function () {
  clearTimeout(timer);
  timer = setTimeout(() => {
    // 模拟触发change事件
    console.log(input.value);
  }, 500);
});
```

节流：限制函数在一定时间内只能执行一次。（大招的冷却时间）

```js
const div1 = document.getElementById('div1');

let timer = null;

div1.addEventListener('drag', e => {
  if (timer) {
    return;
  }
  timer = setTimeout(() => {
    console.log(e.offsetX, e.offsetY);
    timer = null;
  }, 100);
});
```

**常见的应用场景**

防抖：

+ 搜索框输入，只需要用户最后依次输入完再发送请求。
+ 手机号，邮箱格式的输入验证检测。
+ 窗口大小的resize。只需要窗口调整完后，计算窗口的大小，防止重复渲染。

节流：

+ 滚动加载
+ 谷歌搜索框，搜索联想功能。
+ 高频点击提交。



### v-for为什么要加key

vue中列表循环需加:key="唯一标识" 唯一标识可以是item里面id index等，因为vue组件高度复用增加Key可以识组件的唯一性，为了更好地区别各个组件 key的作用主要是为了高效的更新虚拟DOM

无：key属性时，状态默认绑定的是位置
有：key属性时，状态根据key的属性值绑定到了相应的数组元素

**index不能作为key值**



### keep-alive

1. keep-alive是vue内置的一个组件，可以使用包含的组件保留状态，避免重新渲染。
2. 一般结合路由和动态组件一起使用，用于缓存组件。
3. 对应两个钩子函数activated和deactivated，当组件被激活时，触发钩子函数activated，当组件被移除时，触发钩子函数deactivated。
4. 提供include和exclude属性，两者都支持字符串或正则表达式，include表示只有名称匹配的组件会被缓存，exclude表示任何名称匹配的组件都不会被缓存，其中exclude的优先级比include高。



### $nextTick

> vue dom是异步执行的，一旦观察到数据变化，vue就会开启一个队列，然后把同一个事件循环当中观察到数据变化的watcher推送到这个队列。如果这个watcher被触发多次，只会被推送一次。这种缓冲行为可以有效的去掉重复数据造成的不必要的计算和dom操作。而在下一个事件循环时，vue会清空队列，并进行必要的dom更新。
>
> 当我改变dom数据的时候，dom不会立马更新，而是在异步队列中被清除，也就是下一个事件循环开始时执行更新时才会进行必要的dom更新。如果此时你想要根据更新的dom状态去做某些事情，就会出现问题。为了在数据变化之后等待vue完成更新dom，可以在数据变化之后立即使用vue.nextTick。这样回调函数在dom更新完之后就会调用。



作用：将回调延迟到下次DOM更新周期之后执行

下次DOM更新周期：其实是下次微任务执行时更新DOM，而nextTick时将回调添加到微任务中。

**原理**

1. 先定义一个callbacks（回调）存放所有的nextTick里的回调函数。

2. 然后判断一下当前的浏览器内核是否支持Promise，支持就用Promise来触发回调函数。

3. 如果不支持Promise，再判断是否支持MutationObserver（一个可以监听DOM结构变化的接口，观察文本节点发生变化时，触发执行所有回调函数）。

4. 如果不支持MutaionObserver,再判断是否支持setLmmediate。

5. 如果以上都不支持就只能用setTimeout来完成异步执行了。

   延迟调用优先级如下：Promise》MutaionObserver》setlmmdiate》setTimeout



**nextTick里的宏任务和微任务**

关于宏任务，vue先判断是否支持setlmmediate，就是使用setlmmediate；不是就只能用setTimout。

关于微任务，vue会先判断是否支持promise，是就使用Promise，然后判断是否支持MutaionObserver，是就使用MutaionObserver；否则把宏任务赋值给微任务，把宏任务当作微任务执行。



### 解决父子组件执行顺序的问题

> **父beforeCreate->父created->父beforeMount**
>
> **->子beforeCreate->子created->子beforeMount->子mounted**
>
> ->**父mounted。**

```javascript
// 父组件
mounted(){
    window.parentMounted = this._isMounted	// _isMounted是当前实例mouned()是否执行 此时为true
}
// 子组件
mounted(){
    let time=setInterval(()=>{
		if(window.parentMounted){
         	clearInterval(time)
            // 此时父组件的mounted已经执行完毕
            //...
        }
    },500)
}
```



### vue如何监听数组的变化



1. 使用watch 深度监听（性能消耗大，不推荐）

2. 重写数组函数，7种方法。

   ​	在将数组处理成响应式数据后，如果使用数组原始方法改变数组时，数组值会发生变化，但是并不会触发数组的setter来通知所有依赖该数组的地方进行更新，为此，vue通过重写数组的某些方法来监听数组变化，重写后的方法会手动触发通知该数组的所有依赖进行更新。

3. 利用计算属性+ watch

4. 直接监听对象中的属性

5. vue.set()或者this.$set()

   ```javascript
   vue.set(target,key,value)
   //vue.set(修改的值，修改的位置，修改后的参数)
   
   //页面中存在的属性，是可以直接通过赋值的方式更改，因为内部通过Object.defineProperty实现了数据双向绑定，但是对于后面新增的属性，是没有办法渲染的，那么就必须使用Vue.set()
   ```



### 混入 mixin

当多个组件中有相同的方法和处理逻辑，就可以使用 混入mixin。

创建一个minxin.js里定义了混入对象，并通过export导出：在其他组件中导入，直接使用methods中的方法。

```javascript
//在其他组件混入以后，其他组件里就都拥有了, hello方法，并自动在created中执行
export var myMixin = {
    //组件中的其他属性 都可写在这里
    methods: {
        hello: function (msg='') {
            console.log('hello from mixin!' + msg);
        }
    },
    created: function () {
        this.hello();
        // 同名钩子函数将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子之前调用。
        console.log('混入对象-created');
    }
};
```

+ **对于同名的变量和方法，只执行page中的代码。**

+ **混入和page页面代码执行顺序（mixin先执行）**

![img](https://img2020.cnblogs.com/blog/1366381/202108/1366381-20210818163234045-668246168.png)

### webpack

#### webpack核心概念

+ Entry：入口，告诉webpack要使用哪个模块作为构建项目的起点。默认为./src/index.js
+ output：出口，告诉webpack在哪里输出打包的代码以及命名。默认为./dist。
+ Loader：模块转换器，用于把模块原内容按照需求转换成新内容（比如sass转css，Ts转js）。
+ Plugin：插件可以监听这些时间的发生，在特定时机做对应的事情。

#### webpack的工作原理

webpack可以理解是一个模块打包机，它做的事情是，分析你的项目结构，找到JavaScript模块以及其他的一些浏览器不能直接运行的拓展语言（Sass、Ts等），并将其转换和打包为合适的格式供浏览器使用。在3.0出现后，webpack还肩负起了优化项目的责任。



#### webpack的打包原理

把一切都视为模块，不管是css、js、image还是html都可以互相引用，通过定义entry.js对所有的文件进行跟踪，将各个模块通过loader和plugins处理，然后打包在一起。

按需加载：打包过程中webpack通过code Splitting 功能将文件分为多个chunks，还可以将重复的部分单独取出来作为commonChunk，从而实现按需加载。把所有依赖打包成 一个bundle.js，通过代码分割成单元片段并按需加载。



#### webpack的总体打包流程
Webpack首先会把配置参数和命令行的参数及默认参数合并，并初始化需要使用的插件和配置插件等执行环境所需要的参数；初始化完成后会调用Compiler的run来真正启动webpack编译构建过程，webpack的构建流程包括compile、make、build、seal、emit阶段，执行完这些阶段就完成了构建过程。这其实就是我们上面所讲到的。

+ **初始化参数： **从配置文件和 Shell 语句中读取与合并参数，得出最终的参数。

+ **开始编译： **根据我们的webpack配置注册好对应的插件调用 compile.run 进入编译阶段,在编译的第一阶段是 compilation，他会注册好不同类型的module对应的 factory，不然后面碰到了就不知道如何处理了。

+ **编译模块： **进入 make 阶段，会从 entry 开始进行两步操作：第一步是调用 loaders 对模块的原始代码进行编译，转换成标准的JS代码, 第二步是调用 acorn 对JS代码进行语法分析，然后收集其中的依赖关系。每个模块都会记录自己的依赖关系，从而形成一颗关系树。

+ **输出资源：**根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会。

+ **输出完成：**在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统。



## 不常见面试题

### 浮点数相加
  1. 将小数转为整数，相加之后除以相差的倍数
  ```js
    FloatAdd(arg1, arg2) {
      var r1, r2, m
      try {
        r1 = arg1.toString().split('.')[1].length
      } catch (e) {
        r1 = 0
      }
      try {
        r2 = arg2.toString().split('.')[1].length
      } catch (e) {
        r2 = 0
      }
      m = Math.pow(10, Math.max(r1, r2))
      return (arg1 * m + arg2 * m) / m
    },
  ```

### 对象扁平化

```js
function flatObj(o){
	if(typeof o !== 'object') throw new Error(`TypeError:need a object type but get a ${typeof o}`)
    const res={}
    const flat=(obj,preKey='')=>{
        Object.entries(obj).forEach(([key,value])=>{
            let newKey=key
            if(preKey){
                newKey=`${preKey}${Array.isArray(obj)?`[${newKey}]`:`.${newKey}`}`
            }
            if(value && typeof value === 'object'){
                return flat(value,newKey)
            }
            res[newKey]=key
        })
    }
    flat(o)
    return res
}
```





###  < !DOCTYPE / >

https://www.cnblogs.com/better-echo/p/6285301.html

1. doctype的作用

   >< DOCTYPE >  声明位于HTML文档中的第一行，处于<html>标签之前。告诉浏览器用什么文档标准解析这个文档。DOMTYPE不存在或格式不正确会导致文档以兼容模式呈现。

2. 严格模式和混合模式如何区分？他们有什么意思？

   >标准(严格)模式的排版和js运作模式都是以该浏览器支持的最高标准运行。
   >
   >在兼容模式( 混合模式或怪异模式)中，页面以宽松的向后兼容的方式显示，模拟老式浏览器的行为以防止站点无法工作。




### H5新特性

语义化标签：header、footer、article、selection

表单控件：数字、日期、时间、日历、滑块。

图像支持：canvas、svg。

多媒体：video、audio（音频）。



### undefined 和unll的区别

```js
null==undefined  //ture
null===undefined  //false
```

null：代表“空值”，代表一个空对象指针，使用typeof运算得到“object”，所以可以理解为一个特殊的对象值。

undefined：当一个声明的变化未初始化时，得到的值就是undefined。



null表示“没有对象”，即该处不应该有值。典型用法是：

（1）作为函数的参数，表示该函数的参数不是对象。

（2）作为对象原型链的终点。

undefined表示“缺少值”，就是此处应该有一个值，但是没有定义，典型用法是：

（1）变量被声明了，但是没有赋值，就等于undefined。

（2）调用函数时，应该提供的参数没有提供，该参数就等于undefied。

（3）对象没有赋值的属性，该属性的值undefined。

（4）函数没有返回值，默认返回undefined。 





### Watch监听

watch：一个数据影响多个数据。

computed：一个数据受多个数据影响。缓存值，不会主动重新计算，只有存在依赖数据，依赖数据发发生改变才会重新计算。

**如果在handler函数中使用了箭头函数，改变了this指向，就无法获取到Vue实列，则为undefined。所以不要在这使用箭头函数，如果用，let that=this。**

**对于父子组件传参，异步获数据有时会存在获取不到值的情况。这是watch就派上用场，适当的时候配合immediate或者deep属性配合使用**

1. 常用

   ```javascript
   data:{
       name:'王'
   },
   watch:{
   	name:(newVal,oldVal){
           //newVal:表示新的值，oldVal：旧的值，位置不能改变
           conole.log(newVal,oldVal)
       }
   }
   ```

2. immediate、deep、handler属性

   immediate：当值第一次绑定的时候，不会执行监听函数，只有值发生改变才会执行。如果我们需要在最初绑定值的时候也执行函数，就需要用到immediate。

   deep：对于对象或者对象中的属性，可以使用deep。

   handler：使用immediate和deep时才会用。

   ```javascript
   data:{
       obj:{
          	a:'' 
       }
   },
   watch:{
   	obj:{
           hander(newVal,oldVal){
               console.log('newVal-a',obj.a)
               console.log('oldVal-a',obj.a)
           },
           deep:true,//深度监听
           immediate:true//首次加载执行
       }
   }
   ```

3. 监听长度，或者对象属性

   ```javascript
   data:{
       obj:{
          	a:'' 
       },
       arr=[1,2,3,4,5]
   },
   watch:{
   	'obj.a':{//监听对象属性
       'arr.length':{//监听数组长度，最好配合计算属性使用
       '$route':{//监听route变化。
           hander(newVal,oldVal){
               cons.log('newVal-a',obj.a)
               cons.log('oldVal-a',obj.a)
           }
       }
   }
   ```

4. 使用$watch

   ```javascript
   data:{
       obj:{
           a:'1'
       }
   }
   creatd(){
       this.$watch('name',(new,old)=>{
                console.log('new')
   	})
   }
   ```

   



### 单项数据流的理解

vue中子组件可以使用父组件传递过来的数据，但是绝对不能修改传递过来的数据。

强行修改会导致你的应用数据流向难以理解。



### axios和ajax的区别

axios是通过promise实现了对ajax技术的一种封装，就像jQuery实现ajax封装一样。



ajax缺点：

1. 本身是对MVC的编成，不符合现在前端MVVM的浪潮。
2. 基于原生的XHR开发，XHR本身的架构不清晰，已经有fetch的替代方案。

axios优点：

1. 从node.js创建http请求。

2. 支持PromiseAPI。

3. 客户端支持防止CSRF攻击。

4. 提供了一些并发请求的接口（重要，方便了很多的操作）



### Map和Set

ES6新增了两个对象，Map和Set，Map是一组键值对的结构，具有极快的查找速度。Set是一组key的集合，但不存储value，而且key不重复，可自动排重。



**Map**

> Map映射是ES6里面新增的一个对象，是一组键值对的结构，具有极快的查找速度。

```javascript
//初始化Map需要一个二位数组，或者直接初始化一个空Map
var m1=new Map([['a', 'a1'], ['b', 'b2'], ['c', 'c3']]);
var m11 = new Map([['a', 'a1'], ['b', 'b2'], ['c', 'c3']]);
var m2 = new Map();

console.log(m1); //返回Map, {"a" => "a1", "b" => "b2", "c" => "c3"}
console.log(typeof(m1); //object, Map任属于object
console.log(m1=m2);  // false 虽然两个Map里面的值一样，但是是属于不同的object。

//1.size属性、返回Map的元素数
console.log(m1.size); //3

//2.keys()  获取Map的所有key
console.log(m1.keys())  //返回{"a", "b", "c"}

// 3. values()    获取Map的所有value
console.log(m1.values());    // 返回 {"a1", "b2", "c3"}

// 4. entries()    获取Map所有成员  
console.log(m1.entries());// 返回 {"a" => "a1", "b" => "b2", "c" => "c3"}

// 5. forEach()    循环操作映射元素
m1.forEach(function(value, key, map) {
   // value:  key对应的值，  
   // key: Map的key，(map参数已省略情况下，key可省略)
   // map:  Map本身，(该参数是可省略参数)
   console.log(value);           // key对应的值   a1  b2  c3
   console.log(key);         // key          a   b   c
   console.log(map);         // Map本身      Map Map Map
});

// 6. set()        给Map添加数据，  返回添加后的Map
console.log(m2.set('a', 1));    // 返回Map  {"a" => 1}
console.log(m2.set('b', 2));    // {"a" => 1, "b" => 2}
console.log(m2.set('a', 11)); 
// {"a" => 11, "b" => 2} 给已存在的键赋值会覆盖掉之前的值

// 7. has()        检测是否存在某个key， 返回布尔值，有：true； 没有：false
console.log(m2.has('a'));        // true
console.log(m2.has('c'));        // false

// 8. get()        获取某个key的值，返回key对应的值，没有则返回undefined  
console.log(m2.get('a'));        // 11
console.log(m2.get('c'));        // undefined

// 9. delete()    删除某个key及其对应的value，返回布尔值，成功：true； 失败：false
console.log(m2.delete('b'));    // true
console.log(m2.delete('d'));    // false
console.log(m2.get('b'));        // undefined， 因为b已经删除

// 10. clear()    清除所有的值，返回 undefined
console.log(m1.clear());        // undefined
console.log(m1);                // {} 
```



**Set**

> Set是ES6新增的对象，Set是一组key的集合，但不存储value，而且key不重复，可自动排重

```javascript
// 初始化Map需要提供一个Array作为输入，或者直接创建一个空Set
var s1 = new Set(['a', 'b', 'c']);
var s11 = new Set(['a', 'b', 'c']);
var s2 = new Set(['a', 'a', 'b', 'b', 'c', 'c']);
var s3 = new Set();

console.log(s1);                // 返回 Set(3) {"a", "b", "c"}
console.log(s2);                // 返回 Set(3) {"a", "b", "c"}
console.log(typeof(s1));        // object
console.log(s1 == s11);        // false
console.log(s1 == s2);        // false

// 1. size属性  返回Set的元素数
console.log(s1.size);            // 3

// 2. keys() 获取Set的所有key    
console.log(s1.keys());        // 返回 SetIterator {"a", "b", "c"}

// 3. values()  获取Set的值，返回结果和 keys()一样
console.log(s1.values());        // 返回 SetIterator {"a", "b", "c"}

// 4. entries() 获取Set所有成员，返回同keys()
console.log(s1.entries());    // 返回 SetIterator {"a", "b", "c"}

// 5. forEach() 循环操作集合元素    
s1.forEach(function(v, k, s){    // v、k是集合的键，s是集合本身
    console.log(v);               //  a   b   c
    console.log(k);               //  a   b   c
    console.log(s);               // Set Set Set
});
// 6. add()   给集合添加数据    返回添加后的Set
console.log(s3.add('aa'));      // Set(1) {"aa"}
console.log(s3.add('bb'));      // Set(2) {"aa", "bb"}
console.log(s3.add('aa'));      // Set(2) {"aa", "bb"}  添加重复的值，会被排重掉，

// 7. has() 查询集合中是否包含某个元素  返回布尔值 有：true； 没有：false
console.log(s3.has('aa'));        // true
console.log(s3.has('ff'));        // false    

// 8. delete() 删除集合中的某个元素  返回布尔值
console.log(s3.delete('aa'));    // true
console.log(s3.delete('ee'));    // false
console.log(s3);                // Set(1) {"bb"}

// 9. clear()  清除集合的所有值    返回undefined
console.log(s1.clear());        // undefined
console.log(s1);                // Set(0) {}
```





### jQuery

选择器使用

```javascript
$("#text")
```

**节点插入**

append：向每个匹配的元素内部追加内容

appendTo：将所有匹配的元素追加到指定的元素中

after：在每个匹配元素之后插入内容

insertAfter：将所有匹配的元素插入到指定的元素后面

before：在每个匹配的元素之前插入内容

insertBefore：将所有匹配的元素插入到指定的元素的前面

**函数**

get()  取得所有匹配的DOM元素集合

append() 向每个匹配的元素内部追加内容

find()  搜索所有与指定表达式匹配的元素

bind()  为每个元素的特定事件绑定事件处理函数

empty()  删除匹配的元素集合中所有的子节点

hide()  隐藏

**操作样式**

addClass()  来追加样式

removerClass()  来删除样式

toggle()   来切换样式

**$(document).ready()**

当DOM完全加载，就会执行你写的函数。

**window.onload事件和jQuery.ready函数的不同**

window.onlod事件等待DOM被创建，还要等所用的外部资源被引用完毕后，才会执行我的内容。

jQuery.ready函数只需要等待DOM执行完毕后，就会执行。



### Typescript和JavaScript的区别

**JavaScript**

1. 动态类型，运行时明确变量的类型，变量的类型由变量的值决定，并跟随值的改变而改变。
2. 直接运行在浏览器和node.js环境中。
3. 弱类型，数据类型可以被忽略的语言。一个变量可以赋不同数据类型的值。

**Typescript**

1. 静态类型，声明时确定类型，之后不允许修改；
2. 编译运行，始终先编译成JavaScript再运行
3. 强类型，一旦一个变量被指定了某个数据类型，如果不经过强制转换，那就他就永远是这个数据类型了



### http的工作过程

1. 地址解析

2. 封装http请求数据包

3. 封装成TCP包，建立TCP连接(TCP的三次握手)

4. 客户机发送请求命令

5. 服务器响应

6. 服务器关闭TCP链接

   ​	6.1 特殊场景：keep-alive添加此关键词，则可以保持连接。



### export和export default的区别

1. export与export default均可用于导出常量，函数，文件，模块等
2. 在一个文件或模块中，export，import可以有多个，export default仅有一个
3. 通过export方式导出，在导入时要加{}，export default则不需要。

```javascript
//export
//a.js
const str="balbalbal~"
function log(str){console.log('str')}
export { str,log }

//b.js (导出方式)
import {str,log} from 'a'//引入名必须和函数名一致,可以不全引

//export default
//a.js
 const str="balbalbal~"
 function log(str){console.log('str')}
 export default {str,log}

 //b.js
 import name from 'a'//重新命名，直接调用以前方法。
```



### PC端与手机端自适应

+ Bootstrap 这种框架就是依赖媒体查询，实现布局随设备宽度自动切换
+ 字体大小 元素大小都使用rem或em这种相对单位，不使用px固定单位
+ 关键标签：<meta name=”viewport” content=”width=device-width, initial-scale=1″ />
+ 根据屏幕宽度 加载不同的css文件
+ 图片的自动缩放，列入img{max-width：100%；}，根据不同屏幕分辨率加载不同大小的图片



### http与https区别

http协议和https协议的区别：传输信息安全性不同，连接方式不同，端口不同，证书申请方式不同

+ 传输信息安全性不同
  1. http协议：是超文本传输协议，信息是明文传输。如果攻击者截取了Web浏览器和网站服务器之间的传 输报文，就可以直接读懂其中的信息。
  2. https协议：是具有安全性的ssl加密传输协议，为浏览器和服务器之间的通信加密，确保数据传输的 安全。
+ 连接方式不同
  1. http协议：http的连接很简单，是无状态的。 
  2. https协议：是由SSL＋HTTP协议构建的可进行加密传输、身份认证的网络协议。
+ 端口不同
  1. http协议：使用的是端口80
  2. https协议：是以哦那个的端口端口443
+ 证书申请方式不同
  1. http协议：免费申领
  2. https协议：需要到ca申请证书，一般需要交钱。



### apply call bind 的区别

为非**箭头函数**设置函数体中的this对象

```javascript
function demo(wife,phone){
    console.log(`${this.name}的${wife}电话是${phone}`);
}
let obj={name:'然然'}
demo('小乔'，'10086')//undefined的小巧电话是10086
demo.apply(obj,['小乔','10086'])
demo.call(obj,'小乔'，'10086')
let a=demo.bind(obj,'小乔','10086')
a()
```

总结：

+ apply：函数中的this替换成参数1，其余参数放数组中，直接触发函数。
+ call：函数中的this替换成参数1，其余参数依次摆放，直接触发
+ bind：替换函数中的this指向并传入其他参数，返回新的函数，不会直接触发函数



### 浏览器渲染流程

1. 构建DOM：从上到下解析HTML文档生成DOM节点树，也叫内容树。
2. 构建CSSOM树：加载解析样式生产CSSDOM树。
3. 构建JavaScript：加载并执行Javascript（内外联都执行）
4. 构建渲染树：根据DOM树和CSSOM树，生成渲染树。
5. 布局：根据渲染树节点的每一个节点布局在屏幕上正确位置
6. 绘制：便利渲染树绘制所有节点，为每一个节点适用于对应的样式，这一过程是通过UI后端模块完成



### js怎么实现继承，各自优缺点

原型链继承、构造继承、实例继承、拷贝继承、组合继承、寄生组合继承

1. **原型链继承**

   **核心**：将父类的实列作为子类的原型

   ```javascript
   function Cat(){ 
   }
   Cat.prototype = new Animal();
   Cat.prototype.name = 'cat';
   var cat = new Cat();
   console.log(cat.name);
   ```

   特点：

   1. 非常纯粹的继承关系，实例是子类的实例，也是父类的实例
   2. 父类新增原型方法/原型属性，子类都能访问到
   3. 简单，易于实现

   缺点：

   1. 要想为子类新增属性和方法，必须要在`new Animal()`这样的语句之后执行，不能放到构造器中
   2. 无法实现多继承
   3. 来自原型对象的所有属性被所有实例共享（来自原型对象的引用属性是所有实例共享的）（详细请看附录代码： 示例1）
   4. 创建子类实例时，无法向父类构造函数传参

2. **构造继承**

   **核心：**使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类（没用到原型）

   ```javascript
   function Cat(name){
     Animal.call(this);
     this.name = name || 'Tom';
   }
   
   // Test Code
   var cat = new Cat();
   console.log(cat.name);
   ```

   特点：

   1. 解决了1中，子类实例共享父类引用属性的问题
   2. 创建子类实例时，可以向父类传递参数
   3. 可以实现多继承（call多个父类对象）

   缺点：

   1. 实例并不是父类的实例，只是子类的实例
   2. 只能继承父类的实例属性和方法，不能继承原型属性/方法
   3. 无法实现函数复用，每个子类都有父类实例函数的副本，影响性能

3. **实例继承**

   **核心：**为父类实例添加新特性，作为子类实例返回

   ```javascript
   function Cat(name){
     var instance = new Animal();
     instance.name = name || 'Tom';
     return instance;
   }
   
   // Test Code
   var cat = new Cat();
   console.log(cat.name);
   ```

   特点：

   1. 不限制调用方式，不管是`new 子类()`还是`子类()`,返回的对象具有相同的效果

   缺点：

   1. 实例是父类的实例，不是子类的实例
   2. 不支持多继承

4. **拷贝继承**

   ```javascript
   function Cat(name){
     var animal = new Animal();
     for(var p in animal){
       Cat.prototype[p] = animal[p];
     }
     // 2020年10月10日21点36分：感谢 @baclt 的指出，如下实现修改了原型对象，会导致单个实例修改name，会影响所有实例的name值
     // Cat.prototype.name = name || 'Tom'; 错误的语句，下一句为正确的实现
     this.name = name || 'Tom';
   }
   
   // Test Code
   var cat = new Cat();
   console.log(cat.name);
   ```

   特点：

   1. 支持多继承

   缺点：

   1. 效率较低，内存占用高（因为要拷贝父类的属性）
   2. 无法获取父类不可枚举的方法（不可枚举方法，不能使用for in 访问到）

5. **组合继承**

   **核心：**通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

   ```javascript
   function Cat(name){
     Animal.call(this);
     this.name = name || 'Tom';
   }
   Cat.prototype = new Animal();
   
   // 感谢 @学无止境c 的提醒，组合继承也是需要修复构造函数指向的。
   
   Cat.prototype.constructor = Cat;
   
   // Test Code
   var cat = new Cat();
   console.log(cat.name);
   ```

   特点：

   1. 弥补了方式2的缺陷，可以继承实例属性/方法，也可以继承原型属性/方法
   2. 既是子类的实例，也是父类的实例
   3. 不存在引用属性共享问题
   4. 可传参
   5. 函数可复用

   缺点：

   1. 调用了两次父类构造函数，生成了两份实例（子类实例将子类原型上的那份屏蔽了）

6. **寄生组合继承**

   **核心：**通过寄生方式，砍掉父类的实例属性，这样，在调用两次父类的构造的时候，就不会初始化两次实例方法/属性，避免的组合继承的缺点

   ```javascript
   function Cat(name){
     Animal.call(this);
     this.name = name || 'Tom';
   }
   (function(){
     // 创建一个没有实例方法的类
     var Super = function(){};
     Super.prototype = Animal.prototype;
     //将实例作为子类的原型
     Cat.prototype = new Super();
   })();
   
   // Test Code
   var cat = new Cat();
   console.log(cat.name);
   ```

   特点：

   1. 堪称完美

   缺点：

   1. 实现较为复杂




### 项目目录结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191225163735830.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NDEwNzk1,size_16,color_FFFFFF,t_70)





### vue内部指令

v-bind：响应并更新DOM特性

v-on：用于监听DOM事件

v-model：数据双向绑定，用于表单输入等

v-show：条件渲染指令，为DOM设置css的style属性

v-if：条件渲染指令 ，动态在DOM内添加或删除DOM元素

v-else：条件渲染指令，必须跟v-if成对使用

v-for：循环指令

v-else-if：判断多层条件，必须跟v-if成对使用

v-text：更新元素的txtContent

v-html：更新元素的innerHTML

v-pre：不需要表达式，跳过这个元素以及子元素的编译过程，以此来加快整个项目。

v-cloak：不需要表达式，这个指令保持在元素上直到关联实例结束编译

v-once：不需要表达式，只渲染元素或组件一次，随后的渲染，组件/元素以及下面的子元素都当成静态页面不在渲染







### js符号优先级

| 优先级 | 运算符                                                       | 说明                                                   |      |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------ | ---- |
| 1      | []  .   ()                                                   | 字段访问、数组索引、函数调用和表达分组                 |      |
| 2      | ++  --   -   ~   !   delete new  typeof  void                | 一元运算符、返回数组索引、对象创建、未定义的值         |      |
| 3      | *  /   %                                                     | 相乘、相除、求余数                                     |      |
| 4      | +  -                                                         | 相加、相减、字符串拼接                                 |      |
| 5      | <<   >>   >>>                                                | 左位移、右位移、无符号右移                             |      |
| 6      | <    <=   >   >=   instanceof                                | 小于、小于或等于、大于、大于或等于、是否为特定类的实例 |      |
| 7      | ==   !==   ===   !==                                         | 相等、不相等、全等、 不全等                            |      |
| 8      | &                                                            | 按位‘与‘                                               |      |
| 9      | ^                                                            | 按位‘异或’                                             |      |
| 10     | \|                                                           | 按位'或'                                               |      |
| 11     | &&                                                           | 短路与（逻辑 ’ 与 ‘）                                  |      |
| 12     | \|\|                                                         | 短路或（短路 ’ 或 ‘）                                  |      |
| 13     | ?:                                                           | 条件运算符                                             |      |
| 14     | =   +=   -=   *=   /=   %=   &=   \|=   ^=   <   <=  >   >=   >>= | 混合赋值运算符                                         |      |
| 15     | ，                                                           | 多个计算                                               |      |



### import和require和区别

遵循规范

+ require是AMD规范引入方式
+ import是es6的一个语法标准，如果要兼容浏览器的花必须要转为es5的语法。

调用时间

+ require是运行时调用，所以require理论上可以运用在代码的任何地方
+ import是编译时调用，所以必须放在文件开头

本质

+ require是赋值过程，其实require的结果就是对象、数字、字符串、函数等、再把require的结果赋值给某个变量
+ import是解构过程，但是目前所有的引擎都还没有实现import，我们在node中使用babel支持ES6，也仅仅是ES6转为ES5再执行，import语法会被转码为require。



### 代码规范，Eslint是干什么的

基本格式化

+ 常量使用全大写字母，并用下划线分割GLOBAL_NAME="name"
+ 变量和函数小驼峰方式，常量名词开头，函数动词开头。
+ 构造函数class大驼峰方式。
+ 一行代码不超过80个字符，编辑器会换行。
+ 字符串统一使用单引号，多行或需要携带变量使用反引号，props属性参数使用双引号。
+ null当做对象占位符。
+ 避免使用undefined。
+ 创建对象时使用：{}。
+ 创建数组时使用：[]。

**EsLint是javascript代码中识别和报告模式匹配的工具，他的目标时保证代码的一致性和避免错误。**



### v-on监听多个方法

```html
<input type="text" v-on={input:onInput,focus:onFocus,blur:onBlur}>
```



### vue中事件绑定加括号和不加括号的区别

```java
// 不带括号，不写实参。默认传event(事件对象)
@click="fun"

//只要加括号，无论是否传参，都属于传实参给函数，event(事件对象)就接受不到。
@click="fun(value)"

//如果需要传实参，又需要event(事件对象)，就需要手动传入event(事件对象)
@click=fun($event,value)
```



### src和href的区别

1. href标识超文本引用，用再link等元素上，href和a等元素上，href是引用和页面关联，实在当前元素和引用资源之间建立联系。
2. src表示引用资源，表示替换当前元素，用在img，script，iframe上，src是页面内容不可缺少的一部分。

3. src是指向外部资源的位置，指向的内部会迁入到文档中当前标签所在的位置；在请求src资源时会将其指向的资源下载并应用到当前文档中，列入js脚本，img图片和ifame等元素。



### Event loop

javaScript是单线程，所有任务都需要排队，前一个任务结束，才会执行后一个人任务。

而这种**主线程从"任务队列"中读取执行事件，不断循环重复的过成**，就被称为**事件循环（Event Loop）**

1. js用来存储待执行回调函数的队列包含2个不同特点的队列，

2. 宏任务：用来保存待执行的宏任务，比如script全部代码、setTimeout、setInterval、ajax回调。
3. 微任务：用来保存待执行的微任务，比如：promise的回调、MutationObserver的回调。
4. js执行时会区别这2个队列
   1. js引擎首先必须执行所有的初始化同步任务代码。
   2. 每次准备取出第一个宏任务前，都要将所有的微任务一个一个取出来执行。



### for循环中let和var区别

var是全局作用域，有变量提升的作用，所以在for中定义一个变量，全局可以使用，循环中的每一次变量i赋值都是给全局变量i赋值。

let是块级作用域，只能在代码块中起作用，在js中一个{}中的语句我们也称为叫一个代码块，每次循环会产生一个代码块，每一个代码块中的都是一个新变量；



### HTML行内元素和块级元素的区别

1. 可以相互转换，使用display属性进行转换，
2. 行内元素会在一条水平线上排列；块级元素总是独占一行，垂直向下排列，若想水平排列，可以使用浮动。
3. 行内元素不可以设置宽高，但是可以设置行高，margin和padding的上下无效，左右有效。
4. 块级元素可以包含行内元素和块级元素；行内元素不能包含块级元素，只能包含文本元素和行内元素。



### JSON.stringify和qs.stringify的区别

json. 只能在字符串和对象中进行的转换，多用于改变数据类型（类似local sessionStorage只能存储字符串）

qs. 可以将url进行转换，会自动替换&,=等相关字符。

```javascript
let url = 'method=query_sql_dataset_data&projectId=85&appToken=7d22e38e-5717';
console.log(qs.parse(url));
//{
//     method: "query_sql_dataset_data",
//     projectId: "85",
//     appToken: "7d22e38e-5717"
//   };
console.log(JSON.parse(url)) 
//报错，因为url不是字符串
```



### vue2和vue3的区别

1. 默认进行懒观察

​		在2.0版本，不管数据多大，都会在一开始为其创建观察者。当数据很大的时候，这可能会在页面载入时造成明显的性能压力。3.0版本。只会对用于渲染的数据创建观察者，而3.0的观察者更高效。

2. 更精准的变更通知

   举例来说：2.0版本中，是一个vue.set来给对象新增一个属性时，这个对象的所有watcher都会重新运行；3.0版本中，只有依赖那个属性的watcher才会重新运行。

3. 新加了TypeScript以及PWA的支持

4. 部分命令发生改变

   ​	下载安装 npm install -g vue@cli
   　删除了vue list
   　创建项目 vue create
   　启动项目 npm run serve

5. 默认目录结构发生了变化

   移除了配置文件目录，config 和 build 文件夹
     　移除了 static 文件夹，新增 public 文件夹，并且 index.html 移动到 public 中
     　在 src 文件夹中新增了 views 文件夹，用于分类 视图组件 和 公共组件

6. 使用上的变化



### vue修饰符

**事件修饰符**

```html
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>
<!-- 提交事件不在重载页面 -->
<form v-on:submit.prevent:"onSubmit"></form>
<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>
<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.captrue="dothis">...</div>
<!-- 只当在event.target是当前元素自身触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>
<!-- 滚动事件的默认行为(滚动行为会被立即触发) -->
<div v-on:scroll.passive="onScroll">...</div>

//使用修饰符，顺序很重要；相应的代码会以同样的顺序产生。因此，用v-on:click.prevent.self会阻止所有的点击，而v-on:click.sefl.preven只会阻止对元素自身的点击
```

**按键修饰符**

```javascript
<!-- 只有在‘key’是‘Enter’时调用‘vm.submit()’ -->
<input v-on.keyup.enter="submit">
`l`
```

**v-model修饰符**

```html
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg">

<!-- 将用户输入的内容转为数值类型 -->
<input v-model.number="age" type="number">

<!-- 过滤用户输入的前后空白字符 -->
<input v-model.trim="msg">
```



### HTTP协议状态码

浏览器与web服务器之间的通信协议

http返回码：2xx成功，3xx请求重定向，4xx客户端错误，5xx服务器错误。

200-请求成功

301-删除请求数据f

302-其他地址发现了请求数据

303-客户访问了其他URL或访问方式

304-客户端已经执行了GET，但所请求的资源未修改，不会返回任何资源。

404-没有发现文件，查询或URL。

500-内部服务器错误

 

### new的执行过程

使用new关键字调用构造函数Student，分为四步。

1. 在内存中创建了一个实例对象（内容为空）

   ```javascript
   var stu1={}
   ```

2. 设置该实例对象的_ _proto_ _属性执行构造函数的prototype原型对象

   ```javascript
   stu1.__proto__==student.protope
   ```

3. 使用该实列对象stu1调用构造函数，改变构造函数中的this指向为实例对象stu1

   ```javascript
   Student('张三'，20).call(stu1)
   ```

4. 返回刚刚建好的实例对象



### JS常见的内存泄漏

1. 意外的全局变量（全局变量很难被垃圾回收器回收，所以会进行内存泄漏）
2. 被遗忘的计时器或回调函数（忘记中止定时器）
3. 脱离DOM的引用（dom存成了变量，此时同样的dom元素存在两个引用)
4. 闭包

**内存泄漏的识别方法**

+ Chrome浏览器的控制台Performance或Memory
+ Node提供process.memoryUsage方法

**避免内存泄漏**

+ 注意程序逻辑，避免死循环
+ 减少不必要的全局变量或者相对作用域链上的全局变量或者生命周期很长的对象，及时回收
+ 避免频繁创建过多的对象，用完了记得销毁



### 重绘和回流

引起DOM树结构变化，页面布局变化的行为叫回流,且回流一定伴随重绘。

只是样式的变化，不会引起DOM树的变化，页面布局的行为叫重绘，且重绘不一定会伴随回流。



### js浮点数运算精度问题

**产生原因：**

​	当我们把0.1和0.2转为二级制之后，变成了一个无限循环的数字，计算机中是不允许无限循环的，计算机会进行舍入处理。进行双精度浮点数的小数部分最多支持52位，所以两者相加之后得到这么很长一串的数字。因浮点数小数位的限制而截断的二进制的数字，这时候，我们再把它转为十进制，就出现了误差。

**解决方案：**

+ 将结果四舍五入（toFixed）
+ 将浮点数转为整数再将结果除以扩大的倍数
+ 把浮点数转为字符串，模拟实际运算的过程



### 垃圾回收和内存泄漏

**内存泄漏：**不再用到的内存，没有及时释放。

**垃圾回收：**为了避免内存的泄漏，垃圾回收机制会定期找出哪些不再用到的变量，然后释放其内存，

垃圾回收有两种方式 :标记清除（常用）、引用计数。

+ 标记清除

  当变量进入环境时，就将这个变量标记为"进入环境"，当变量离开环境时，则将其标记为“离开环境”，离开环境，自动被回收。

+ 引用计数

  语言引擎有一张“引用表”保存了内存里面所有资源的引用次数，如果一个值的引用次数为0，就表示这个值没有用到了，就会被内存释放。



### 漏洞防御

+ xss跨站脚本攻击（原理，如何进行的，防御手段是什么）
+ CSRF跨站请求伪造（如何防伪造，怎么防御，等等都要说清楚）
+ sql脚本注入（注入方式，防御方式） 
+ 上传漏洞（防御方式）



### 前端数据加密方法

+ md5加密
+ base64加密
+ sha1加密
+ RSA加密



###  router和route的区别

1. $router时vueRouter的一个对象，通过router的实列对象，这个对象是一个全局的对象，他包含了所有的路由，包含了许多关键的对象和属性。

   $router.push({path:'home'})，本质是向history栈中添加一个路由，在我们看来是切换路由，但本质是在添加一个history记录。

   $router.replace({path:'home'})，替换路由，没有历史记录

2. $route是一个跳转的路由对象，每个路由都会有一个$route对象，是一个局部的对象，可以获取对应的name，path，params，query，router，matchd等。




### vue-router路由传参的几种方式

1. get方法
  ```js
      <router-link :to="{path:'/test',query: { userId: 123,userName:'xia' }}">跳转</router-link>
      或
      <router-link :to="{name:'test',query: { userId: 123,userName:'xia' }}">跳转</router-link>
      //接收值（页面刷新的时候不会消失）
      this.$route.query.userId  // 123
      this.$route.query.userName  // xia
      // url上显示参数：http://localhost:8080/test?userId=123&userName=xia
  ```
2. post方法
  ```js
    <!-- 必须用 name:'test' -->
    <router-link :to="{name:'test',params: { userId: 123,userName:'xia' }}">跳转</router-link>

    <!-- 用 path:'/test' 无效 -->
    <!-- <router-link :to="{path:'/test',params: { userId: 123,userName:'xia' }}">跳转</router-link> -->
    // 接收值（页面刷新的时候就会消失）
    this.$route.params.userId  // 123
    this.$route.params.userName  // xia
    // url上不显示参数：http://localhost:8080/test
  ```
3. 路由方法
  ```js
      // router.js
    {
        path: '/test/:userId/:userName?', //?问号的意思是该参数不是必传项
        name: 'test',
        component: 'test.vue',
        props: true,
    },
    // App.vue
    <router-link to="/test/123/xia">跳转</router-link>
    // 接收值（页面刷新的时候不会消失）
    this.$route.params.userId  // 123
    this.$route.params.userName  // xia
    // url上显示参数：http://localhost:8080/test/123/xia
  ```

### js语句和表达式的区别

  #### 表达式：会产生一个值，可以放在任何地方，（vue template中只能写表达式）
    下面这些都是表达式：
    1. a.
    2. a+b
    3. demo(1)
    4. arr.map(1)
    5. function test(){}

  #### 语句：就是在js中写的代码
    1. if(){}
    2. for(){}
    3. switch(){}
    4. forEach()

### Object中的方法

> javascript中object方法：assign()、create()、entries()、freeze()、getPrototypeOf()、is()、keys()、seal()、values()、isSealed()等等。

+ Object.assign(targetObject,obj1,obj2...)
  用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。
  ```js
    // 单组示例
    const obj1={a:1,b:2};
    const obj2={c:3,d:4};
    const obj=Object.assign(obj1,obj2);
    console.log(obj);// {a: 1, b: 2, c: 3, d: 4}
    console.log(obj===obj1);// true
    // 多组示例
    const obj3={e:5,f:6};
    const obj4={g:7,h:8};
    const objMore=Object.assign(obj,obj1,obj2,obj3,obj4);
    console.log(objMore);// {a: 1, b: 2, c: 3, d: 4, e: 5, f: 6, g: 7, h: 8}
    console.log(objMore===obj); // true
  ```

+ Object.values(obj)
  获取对象的可遍历属性值(值)
    ```js
        const obj={name:'tom',age:30};
        const res=Object.values(obj);
        console.log(res);// ["tom", 30]
        // 当参数为字符串的情况
        const str='Hello';
        const strRes=Object.values(str);
        console.log(strRes);// ["H", "e", "l", "l", "o"]
    ```

+ Object.entries(obj)
  获取对象的可遍历键值对
  ```js
    const obj={name:'tom',age:30};
    const res=Object.entries(obj);
    console.log(res)；// [['name','tom'],['age',30]]
  ```

+ Object.keys(obj)
  获取对象的可遍历属性(键)；
  ```js
    const obj={name:'tom',age:30};
    const res=Object.keys(obj);
    console.log(res);// ["name", "age"]
  ```

+ Object.is(val1,val2)
  比较两个值是否相同。所有NaN值都相等(与==和===不同)
  ```js
    // 相同：undefined，null，true,false,指向同一个对象，数字，字符串，+0，-0，NaN。
  ```

+ Object.defineProperties(obj,props)
  给对象添加多个属性并分别指定它们的配置。
  ```js
    // 通俗说明:Object.defineProperties(obj, props)===
    // Obj(构造函数).prototype.方法名/属性名=props;
    // 普通示例
    var obj = {};
    Object.defineProperties(obj, {
        'property1': {
            value: true,
            writable: true
          },
          'property2': {
            value: 'Hello',
            writable: false
          }
        });
    // vue示例
    Object.defineProperties(Vue.prototype, {  
        $http: {    
            value: axios,    
            writable: false  
        }, 
        $api  $api: {    
            value: API,    
            writable: false  
        }
    })
  ```

+ Object.getPrototypeOf(obj)
  返回其原型的对象。

+ Object.setPrototypeOf(obj, prototype)
  改变某个对象实例的原型对象
  ```js
    // 通俗说明：Object.setPrototypeOf(obj, prototype)===
    // obj._proto_=prototype;
    // 构造函数
    function Student(sname,sage){
      this.sname=sname;
      this.sage=sage;
    }
    // 新实例
    const hmm=new Student('hmm',19);
    hmm.bal;// undefined
    // 新对象(后续作为原型对象用的)
    const superFather={ bal:10000000000, car:"infiniti" };
    // hmm的原型对象设置为superFather
    Object.setPrototypeOf(hmm,superFather);
    hmm.bal;// 10000000000
  ```

+ Object.getOwnPropertyDescriptor(obj,'name')
  返回对象指定的属性配置。

+ Object.defineProperty(obj,'name',{})
  给对象添加一个属性并指定该属性的配置。


+ object.getOwnPropertyNames()
  返回一个数组，它包含了执行对象所有可枚举或不可枚举的属性名。

+ Object.getOwnPropertySymbols()
  返回一个数组，它包含了指定自身所有的符号属性。

+ Object.freeze(obj)
  冻结对象：其他代码不能删除或更改任何属性。

+ Object.isEctensible()
  判断对象是否可扩展。

+ Object.isFrozen(obj)
  判断对象是否已经冻结。

+ Object.isSealed(obj)
  判断对象是否已经密封。

+ Object.preventExtensions(obj)
  返回对象的任何扩展。

+ Object.seal(obj)
  防止其他代码删除现有属性。

+ Object.create(father,obj)
  使用指定的原型对象和属性创建一个新的对象。




### npm、cnpm、yarn的区别
  1. npm: 网速慢。容易造成版本不统一。输出内容长。
  2. cnpm: 网速快。淘宝对npm的拷贝，10分钟同步一次。
  3. yarn: 以前安装过，后期可以离线安装。版本统一。扁平模式（将依赖包的不同版本归结为单个版本，以避免创建多个副本）

## 简答题



### 1到100 使用递归

```js
function add(n){
    if(n===1) return 1
    return add(n-1)+n
}
//简单的方式
function add(n){
    return (1+n)*n/2
} 
```



### axios请求拦截器 显示加载状态

```js
//vue页面当中

created(){
    axios.interceptors.request.use((config)=>{
		// 请求拦截
		this.loading=true;
		return config;
	})
	 axios.interceptors.response.use((config)=>{
		// 响应拦截
		this.loading=false
		return config;
	})
}
```



### 做过哪些组件封装

1. 工具函数的封装
   1. 获取时间的方法，时间相减。
   2. 对象扁平化。
   3. localStorage方法，存储对象。
   4. axios封装
      1. 在headers中添加token
      2. data中添加时间戳
      3. 根据后端返回的code码判断用户权限，没有权限返回登录页面。
2. 组件封装
   1. Echarts图表封装（自定义数据格式，大小自适应）
   2. Element表格封装



### Event loop

1. 首先执行主任务：直接打印的、promise。
2. 微任务：.then、
3. 宏任务：setInterval、setTimeout、ajax回调。
4. 然后宏任务，微任务重复循环

```js
setTimeout(function() {
    console.log('1');
},0)
new Promise(function(resolve) {
    console.log('2');
    resolve();
}).then(function() {
    console.log('3')
}).then(function() {
    console.log('4')
})
console.log('5')
// 2 5 3 4 1 


//第二题
console.log('1');
setTimeout(function() {
    console.log('2');
    process.nextTick(function() {
        console.log('3');
    })
    new Promise(function(resolve) {
        console.log('4');
        resolve();
    }).then(function() {
        console.log('5')
    })
})
process.nextTick(function() {
    console.log('6');
})
new Promise(function(resolve) {
    console.log('7');
    resolve();
}).then(function() {
    console.log('8')
})
setTimeout(function() {
    console.log('9');
    process.nextTick(function() {
        console.log('10');
    })
    new Promise(function(resolve) {
        console.log('11');
        resolve();
    }).then(function() {
        console.log('12')
    })
})
//1 7 6 8 2 4 3 5 9 11 10 12
```







## 未解决的问题


> > 浏览器进程和线程

> > 从输出URL到页面加载发生了什么

> > 前端异常监控



> > 面试官问的题

观察者模式是怎么理解的。

webpack除了编译，其他方法用过吗



webpack都经过了哪几个过程

axios请求都经过了哪几步操作

请求拦截实现方式。

vuex生命周期

微信小程序如何存储数据

vue3的理解，一句话解释（朝reatc靠拢）

ts的理解（泛型）

diff算法
分为两种
vue2
1. 判断是不是同一个元素，不是同一个元素，直接替换
2. 是同一个元素=》比对属性=》比对儿子（1.老的有子节点，新的没有 2.新的有子节点，老的没有 3.文本的情况 4.都有children）=》 双指针：头头，尾尾，头尾，尾头=》对比查继续复用

vue3
采用最长递增子序列




双向即时通信的方法
1. websockets
2. 长轮循
3. k8s的list-watch


## 待优化项
循环方式，没写清楚，
porams的理解
es6解构赋值使用场景
true和false是怎么判断的
项数据流的理解
axios为什么要二次封装
http的工作过程
v-on监听多个方法
qiankun微服务
Object方法

复制数组的方法

1. 在ES5中，开发者们经常使用concat()方法来克隆数组

```js
// 在 ES5 中克隆数组(concat()方法的设计初衷是连接两个数组，如果调用时不传递参数就会返回当前函数的副本)
const colors = [ "red", "green", "blue" ];
const clonedColors = colors.concat();
console.log(clonedColors); //"[red,green,blue]"
```

2. 在ES6中，可以通过不定元素的语法来实现相同的目标

```js
// 在 ES6 中克隆数组
const colors = [ "red", "green", "blue" ];
const [ ...clonedColors ] = colors;
console.log(clonedColors); //"[red,green,blue]"
```

3. 使用fill创建相同长度数组，然后使用splice剪切原数组，（会改变原数组）

```js
// 
const colors = [ "red", "green", "blue" ];
const clonedColors = new Array(colors.length).fill(0)
clonedColors.splice(0,colors.length,...colors);
console.log(clonedColors); //"[red,green,blue]"
```

4. 使用Array.from()

```js
const colors = [ "red", "green", "blue" ];
const clonedColors=Array.from(colors)
console.log(clonedColors); //"[red,green,blue]"
```

npm 安装  --save   -g   是什么意思

vue新建页面，methods: ，有些是函数，有些是对象呢
	
工具函数的使用 monment
	
	
	
 el-image 组件导致本地图片不显示的问题
 ```vue 
 <!-- 解决方案 -->
  <el-image :src="require('../assets/bg_login.jpeg')"></el-image>
 ```