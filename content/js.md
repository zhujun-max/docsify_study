
## 基础题

### promise和await/async的区别


区别主要在于按顺序调用多个 异步函数 时的写法 和报错获取 


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

 

### 同步和异步
**同步**: 先执行完当前行内容，然后再执行下一条内容，会阻止后续代码执行，通过返回值获取结果  
**异步**: 把要执行的内容以回调函数形式放入到事件队列，不会阻止后续代码执行，通过回调函数获取结果  

### Promise对象
Promise 是异步编程的一种解决方案    

**有三种对象**：
pending（进行中）、fulfilled（成功）和rejected（失败）


Promise接收两个参数，resolve, reject  
promise是同步，then是异步  

**Promise 的基本使用**
1. then 链式操作，正确时执行。（里面可以传递两个参数，就是成功和错误，写法和then.catch一样，但是在ES2015（ES6）之后，.then()的第二个参数（错误处理函数）逐渐被.catch()方法取代，因为.catch()提供了一种更清晰、更集中的错误处理方式。）
2. catch 链式操作，错误时执行（如果执行resolve的回调出错，也会执行catch）
3. finally 不管最后的状态如何，都会执行的操作
4. all 所有的接口请求完毕后才会执行回调（只要有一个接口失败就走catch，会返回第一个错误的参数，后续不会再执行）(结果是数组，按照接口请求顺序排序)
5. race 所有的接口，谁第一个执行完毕就执行回调（和all类似，all是执行完所有，race是执行完第一个，不管正确或错误）

  **其中一个promise出错，如何保证all执行**  
  在promise.all队列中，使用map滤每一个promise任务，其中任意一个报错后，return一个返回值，确保promise能正常执行走到.then中
  ```js
    var p1 = new Promise((resolve, reject) => {
      resolve('p1');
    });
    var p2 = new Promise((resolve, reject) => {
      reject('p2');
    });
    var p3 = new Promise((resolve, reject) => {
      resolve('p3');
    });
    Promise.all([p1, p2, p3].map(p => p.catch(e => '出错后返回的值' )))
      .then(values => {
        console.log(values);
      }).catch(err => {
        console.log(err);
      })
      // ["p1","出错后返回的值","p3"]
  ```

###  简述ES6使用到的新语句

1. let：块级作用域，不能重复声明，没有变量提升
2. const：常量；声明必须赋值，声明后的**基本数据类型无法被篡改**，引用类型可修改
3. 模板字符串
4. 解构赋值：let {name,age}={name:'dongdontg',age:33}
5. ... ：扩展运算符，代替arguments变量，接受函数的多余参数。function name(...age){}
6. 箭头函数：匿名函数，this永远指向其父作用域，不能用new创建，不能使用arguments
7. Promise：异步编程的一种方案，解决回调地狱
8. class 面向对象


### JSLabel语法
使用label语句可以在代码中添加标签，以便循环时可以退出循环。

```js
  // 使用标记语法 (label) 
  // 标记a(任意名字)相当于外层循
  {
      a: for (let i = 0; i < 20; i++) {
          for (let j = 0; j < 10; j++) {
              if (i === j) {
                  console.log(1)
                  break a; // break 要终止标记 a
              }
          }
      }
  }
```



### 闭包

闭包函数：声明一个函数中的函数，叫做闭包函数

闭包：内层函数引用的外层函数作用域对象，导致外层函数的作用域对象在被调用后无法释放

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

浏览器从一个域名的网页去请求另一个域名的资源。当协议、域名或端口中有任意一个不同时，就会产生跨域问题。  

常见的解决方案有3种：

+ cors

  + 由服务器解决，添加cors功能模块
  + 前端：无操作

+ jsonp：利用script脚本的src不受同源策略限制的特点（只能使用get）

  + 服务器：返回特定的jsonp格式数据

  + 前端：发送特定的jsonp格式数据到服务器

  ```html
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

      <script type="text/javascript" src="https://xxxx.com/try/ajax/jsonp.php?jsoncallback=callbackFunction"></script>
  
  ```

+ 代理proxy（线上使用nginx）

  + vue、angualr都提供固定的方式设定代理

    ```js
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

### 箭头函数和普通函数的区别

1. 语法简洁性

相对于普通函数，箭头函数不用写`function`，有时候还可以省略`{}`和`return`，当只有一个参数时，`（）`也可以省略。
```js
//普通函数
function add(a,b){
     return a+b
}
//箭头函数
const add=(a,b)=>a+b

```

2. this指向不同

普通函数的`this`是在函数被调用时就确定的，它指向调用该函数的对象；    
箭头函数的`this`永远指向其（创建时的）父级的作用域（call、apply、bind也无法改变）

（1） 普通函数      
+ this指向全局对象      
作为函数独立调用时，this 一般指向全局对象（在浏览器中是 window，在Node.js中是 global）      
```js
function func() {
  console.log(this); // window 或 global
}
func();
```
+ this指向调用它的对象      
当函数被对象调用时，this指向调用它的对象。

```js
const obj = {
  name:'dog',
  method: function() {
    console.log(this); // { name: 'dog', method: [Function: method] }
    console.log(this.name);//dog
  }
};
obj.method();

```

+ this指向参数

使用 `call 、 apply、bind `方法调用时，`this` 指向 `call、apply、bind` 方法的第一个参数。

```js
function foo(a,b) {
  console.log(this) //[Number: 1]  
}
foo.call(1,2)

```

+ this指向实例化对象    
在构造函数里面的`this`指向实例化出来的对象

```js
function Constructor() {
  this.value = 'Hello';
}
const instance = new Constructor();
console.log(instance.value); // Hello

```

（2）箭头函数

指向window、指向父级作用域的`this`    

+ this指向`window`    
this指向父级作用域的`this`，当父级作用域为全局作用域时，`this`指向`window`，此时`this.name`为`undefined`。

```js
const obj={
    name:"a",
    fun:()=>{
        console.log(this.name)//undefined
    }
}
obj.fun()

```

+ 箭头函数的this指向父级作用域的this

```js
function foo() {
  console.log(this) // { a: 1, foo: [Function: foo] }
  var test = () => {
      console.log(this) // { a: 1, foo: [Function: foo] }
  }
  test()
}
var obj = {
    a: 1,
    foo: foo
}
obj.foo()
```

（3）总结     
  普通函数的this指向调用该函数的对象      
    ①　独立调用时，指向全局对象（window或global）     
    ②　被对象调用时，指向调用它的对象     
    ③　使用call、apply或bind方法调用时，指向他们的第一个参数      
    ④　在构造函数中使用时，指向实例化该构造函数的对象     

  箭头函数的this指向该函数定义是所在的定义域      
    ①　在全局作用域定义时，this指向window，此时this.item为undefined     
    ②　在普通函数中定义时，this继承普通函数的this指向     

3、有无arguements对象   
(1)普通函数有`arguements`对象   
在普通函数中，可以使用`arguements`对象访问函数的所有对象，它是一个类数组对象。

```js
function fun(){
    console.log(arguments[0]) //1
    console.log(arguments[1]) //2
    console.log(arguments[2]) //3
}
fun(1,2,3);
```

(2)箭头函数无arguements对象   
箭头函数没有自己的 arguments 对象，但可以通过 rest 参数语法来获取所有参数。

```js
const myArrowFunction = (...args) => {
  console.log(args); // 输出传递给函数的参数数组
};

myArrowFunction(1, 2, 3); // 输出: [1, 2, 3]
```

<details> 
  <summary>箭头函数的args和普通函数的arguments的区别</summary>

  **箭头函数的args（通常使用...args表示rest参数）和普通函数的arguments对象在功能和用途上是相似的，但它们在语法和行为上存在显著的区别。以下是对这两者区别的详细解释：**
  1. 语法区别
    + 箭头函数的rest参数（...args）：
        + 箭头函数本身没有arguments对象，但可以使用rest参数语法...args来捕获所有传递给函数的参数。
        + Rest参数是一个数组，它包含了传递给函数的所有参数。
        + Rest参数必须放在函数参数列表的最后。  
    + 普通函数的arguments对象：
        + 普通函数有一个arguments对象，该对象是一个类数组对象，包含了传递给函数的所有参数。
        + arguments对象不是数组，但它具有数组的长度属性，并且可以使用索引来访问各个参数。
        + arguments对象还包含了一些额外的属性，如callee（指向当前执行的函数）和caller（指向调用当前函数的函数，但在严格模式下为null）。
  2. 行为区别
    + 箭头函数的rest参数：
        + 由于箭头函数没有自己的this和arguments，因此rest参数是获取所有参数的唯一方式。
        + Rest参数是一个真正的数组，可以使用数组的所有方法和属性。
    + 普通函数的arguments对象：
        + arguments对象虽然类似于数组，但它不是数组，因此不能直接使用数组的方法（如push、pop等）。不过，可以通过Array.  prototype.slice.call(arguments)等方法将其转换为数组。
        + arguments对象能够反映出函数被调用时传入的参数，即使函数声明时的形参与实际传入的参数不一致。
  3. 使用场景
    + 箭头函数的rest参数：
        + 常用于需要处理不定数量参数的箭头函数中。
        + 由于箭头函数通常用于简短的回调或内联函数，rest参数提供了一种简洁的方式来捕获所有参数。
    + 普通函数的arguments对象：
        + 在需要访问所有传递给函数的参数，而不仅仅是某些特定参数时非常有用。
        + 在函数体内部，当参数数量不确定或需要动态处理参数时，arguments对象非常有用。
  4. 注意事项
      + 在箭头函数中，由于this和arguments的绑定行为与普通函数不同，因此不能期望在箭头函数内部使用arguments对象来获取参数。
      + 在普通函数中，虽然arguments对象提供了很大的灵活性，但也要注意其不是真正的数组，可能会在某些情况下导致性能问题或代码可读性问题。
</details>


4、是否能作为构造函数   
（1）普通函数可以作为构造函数   
普通函数可以用作构造函数，可以通过new关键字来创建实例化对象。

```js
function Person(name){
    this.name=name
}
const p=new Person('dog')
console.log(p.name)//dog
```

(2)箭头函数不能作为构造函数
```js
const Person=(name)=>{
    this.name=name
}
const p=new Person('hh')
console.log(p.name)//ERROR

```

**简要回答：**
1. 箭头函数没有自己的 this、arguments、super 或 new.target 绑定。这些值从外围作用域（即封闭的执行上下文）继承而来。
2. 由于箭头函数不绑定自己的 this，它们不能用作构造函数，因此也没有 prototype 属性。
3. 箭头函数因为没有 prototype 和其他与对象相关的特性，通常比普通函数占用更少的内存。


### 对象、方法、函数的区别和用法

#### 对象：

  **定义：**
    对象是属性（键值对）和方法的集合，用来存储和组织数据。

  **特点：**    
  + 是一种数据结构，可以动态添加属性或方法。
  + 属性是值（数字、字符串、布尔值等）。
  + 方法是对象的行为（函数作为属性）。

  **用法：**
  1. 定义和操作属性：

  ```javascript
    const person = { name: 'Alice', age: 25 }; // 定义对象
    console.log(person.name); // 获取属性：Alice
    person.gender = 'female'; // 动态添加属性
    console.log(person); // { name: 'Alice', age: 25, gender: 'female' }
  ```
  2. 存储和组织复杂数据：

  ```javascript
    const car = {
        brand: 'Toyota',
        model: 'Camry',
        features: ['AC', 'GPS', 'Bluetooth'],
    };
    console.log(car.features[1]); // 获取数组中的值：GPS
  ```
  3. 嵌套对象：

  ```javascript
    const user = {
        name: 'Bob',
        address: { city: 'New York', zip: '10001' },
    };
    console.log(user.address.city); // New York
  ```

#### 方法 

**定义：**
方法是对象的属性，值为函数，表示对象可以执行的行为。

**特点：**
  + 方法是对象的“行为”部分，与属性的“数据”部分相对应。
  + 方法可以通过 this 关键字访问对象的其他属性。

**用法：**
1. 定义方法：

```javascript
const person = {
    name: 'Alice',
    greet: function() { // 定义方法
        console.log('Hello, ' + this.name);
    },
};
person.greet(); // 调用方法：Hello, Alice
```
2. 简写方法：

```javascript
const calculator = {
    add(a, b) {
        return a + b; // 方法简写
    },
};
console.log(calculator.add(2, 3)); // 5
```
3. 操作对象的属性：

```javascript
const counter = {
    count: 0,
    increment() {
        this.count++; // 修改对象属性
        console.log(this.count);
    },
};
counter.increment(); // 1
counter.increment(); // 2
```
#### 函数
**定义：**
函数是一个可调用的代码块，可以独立于任何对象执行任务。

**特点：**
  + 是一种代码复用的方式。
  + 可以接收参数，返回结果。
  + 在 JavaScript 中，函数本身也是对象。

**用法：**

1. 定义和调用函数：
```javascript
function add(a, b) {
    return a + b; // 返回值
}
console.log(add(2, 3)); // 5
```
2. 函数表达式：

```javascript
const greet = function(name) {
    return 'Hello, ' + name;
};
console.log(greet('Alice')); // Hello, Alice
```

3. 匿名函数：

```javascript
setTimeout(function() {
    console.log('Time is up!');
}, 1000); // 1 秒后输出
```
4. 箭头函数：

```javascript
const square = (x) => x * x;
console.log(square(4)); // 16
```


### 构造函数，原型对象，原型、原型链。都是干什么的，怎么区分？


#### 构造函数（Constructor Function）

**构造函数允许你定义一个模板，然后基于这个模板创建多个对象实例。每个实例都有自己的属性副本（除非属性是引用类型，如对象或数组），但它们共享通过原型链继承的方法。**

构造函数的名字通常以大写字母开头，以区别于普通函数。在调用时，使用new关键字

```javascript
// 定义一个构造函数
function Person(name, age) {
    this.name = name;
    this.age = age;
}

// 在原型上添加一个方法
Person.prototype.greet = function() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
};

// 创建两个对象实例
const alice = new Person('Alice', 30);
const bob = new Person('Bob', 25);

// 调用原型上的方法
alice.greet(); // 输出: Hello, my name is Alice and I am 30 years old.
bob.greet();   // 输出: Hello, my name is Bob and I am 25 years old.

```


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



### get和post的区别

+ **get在浏览器回退时是无害的，而post会再次提交请求**
+ get产生的url地址可以被Bookmark（标签标记、收藏为书签），而post不可以
+ get请求会被浏览器主动cache，而post不会，除非手动设置
+ get请求只能进行url编码，而post支持多种编码方式
+ **get请求参数会被完整保留在浏览器历史记录里，而post中的参数不会被保留**
+ **get请求在url中传送的参数时有长度限制的，而post没有**
+ 对参数的数据类型，get只接受ASCII字符，而post没有限制
+ get比post更不安全，因为参数直接暴露在url中，所以不能用来传递敏感信息
+ **get参数通过url传递，post放在Request body中**



### 前端的存储方式

localStorage：没有时间限制，永久存储，永不失效，除非手动删除，每个域名只有5兆（键也占空间），使用windown.localStorage可以检测，同域名多窗口共享（容易出现串数据）。(IE只有3兆，其他的是5兆)

sessionstorage：使用方法和localStrage一样，区别在于sessionStorage浏览器关闭后即被删除。（在该标签或窗口打开一个新页面时会复制顶级浏览器会话的上下文作为新会话的上下文）
（就是说window.open或者a标签跳转的页面会复制之前的sessionstorage到下一个页面）

IndexedDB：浏览器数据库，大于250兆，手动更新      

web sql: 页面刷新就丢失(不常用，基本要废弃)   

token：把你要存储的用户信息加上算法，加上自己知道的密钥，做成一个签名，就形成一个token，别人不知道密钥，就无法伪造。

cookie：在客户端保存用户信息，保存的是String类型，cookie可以保存在客户端，保存不重要的信息，只能存4k。会携带在请求头中，而每次发送请求都会传输，浪费宽带。

session：在服务端保存用户信息，保存的是Object类型，会话结束而销毁，保存重要信息。




### 离线存储哪些方式，各自适应的环境有哪些

localStorage：键值对的方式存储，永久存储，永不失效，必须手动删除，每个域名5M，不安全;

sessionStorage:数据在浏览器关闭后自动删除，5M;

cookies：缺点是请求头带着数据，4k;

Service Worker 和 Cache API：将指定页面缓存到本地。

~~Application Cache：将指定页面缓存到本地，5MB（已被现代浏览器废弃）~~;

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

`e.stopPropagation()`冒泡机制下，阻止事件的进一步往上冒泡。捕获机制下，阻止事件的进一步向下捕获。

`e.cancelBubble` 是`e.stopPropagation()` 的曾用名，也可以阻止冒泡和捕获
`e.cancelBubble = true;`

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


### npm安装时-g、-S、-D有什么区别
**npm install name**：安装依赖到 node_modules 目录下,不写入节点, npm install 时不下载该依赖。

**npm install -g name**：全局安装,不在 node_modules 目录下,不写入节点, npm install 时不下载该依赖。

**npm install name -S**：npm install name -save的简写，自动把模块和版本添加到dependencies(生产环境)。

**npm install name -D**：npm install name -save-dev简写自动把模块和版本添加到devDependencies(开发环境)。

比如：

**构建工具**：gulp和webpakc是用来压缩代码，打包需要的工具，程序实际运行中时候并不需要，就要放在dev中所以要用 -D。

**项目插件**：如element ui ,echarts,这种的插件要在运行中使用的，就要放在dep中所以就用-S。 一般我们项目插件，在api中都可以看到，一般都是-S。因为这些插件是在程序运行中使用的。


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

**Object.prototype.toString.call(x)**   
  + 使用：`Object.prototype.toString.call(2)`         
  + 注意：全部可以判断

**typeof**:       
  + 使用：`typeof 2`    
  + 注意：不能区分object array null，返回值都是object。

**constructor**:  
  + 使用： `(2).constructor === Number`         
  + 注意：null和undefined无原型对象，所以判断不了

**instanceof**:  
  + 使用： `2 instanceof Number`    
  + 注意：可以正确判断引用类型，基础数据类型不能判断



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

### 构造函数与普通函数的区别
构造函数也是一个普通函数，创建方式和普通函数一样  
1. 调用方式不一样    
  普通函数：Fun()  
  构造函数：var F=new Fun()

2. 作用也不一样  
  构造函数用来新建实例对象 

3. 首字母大小写习惯  
  普通函数：首字母小写  
  构造函数：首字母大写

4. 函数this的指向不同  
  普通函数：严格模式undefined，非严格模式window  
  构造函数：在创建对象前没有具体指向谁，创建对象后才具体指向它创建的对象。

5. 写法不同  
  普通函数：使用return  
  构造函数：使用new，不使用return

### delete和Vue.delete删除数组的区别
delete：普通的delete删除一个数组中的元素，该元素会成为空值。数组长度不变。  
vue.delete：删除会直接删除一个数组元素，长度会减少。
```js
  var a=[1,2,3,4]
  var b=[1,2,3,4]
  delete a[1]
  console.log(a)//[1,empty,3,4]
  this.$delete(b,1)//同vue.delete
  console.log(b)//[1,3,4]
```
### 原型与原型链

1. 为所有子对象保存共有方法的对象，成为原型对象。

2. 一个类型中，prototypr和_ _propo_ _其实指向的是同一个原型对象。

   1. prototypr属于构造函数对象，是站在和原型对象平级的位置，查找构造.prototypr.
   2. _ _propo_ _属于每个子对象，是站在子级角度，称呼父对象。

   **访问原型对象：**构造函数.prorotypr

   **访问父对象：**子对象._ _propo_ _
  ![q6JFq1](https://s1.imagehub.cc/images/2024/11/03/ba25088de9e47be2554be31742cd3e8b.png)

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
    // [1,2,2,[45,6,76,null],'afds',565,[34,6,8,9]].toString()   '1,2,2,45,6,76,,afds,565,34,6,8,9'
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

防抖：抖动完之后才执行。   

+ 搜索框输入，只需要用户最后依次输入完再发送请求。
+ 手机号，邮箱格式的输入验证检测。
+ 窗口大小的resize。只需要窗口调整完后，计算窗口的大小，防止重复渲染。

节流：过一段时间执行一次。   

+ 滚动加载
+ 谷歌搜索框，搜索联想功能。
+ 高频点击提交。


### 数组去空值
1. 使用filter
```js
  myArray=['11',23,'',43,'454',4,'443',,43]
  myArray = myArray.filter(function(n) { return n; });
  //['11', 23, 43, '454', 4, '443', 43]
```

### 深拷贝
1. 循环判断添加
2. JSON.parse(JSON.stringify(obj))
3. jQuery的extend方法实现深拷贝
4. Object.assign(obj1, obj2)。一级属性是深拷贝，二级是浅拷贝
5. 扩展运算符。一级属性是深拷贝，二级是浅拷贝

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

   < !DOCTYPE >声明叫做文件类型定义（DTD），声明的作用为了告诉浏览器该文件的类型。让浏览器解析器知道应该用哪个规范来解析文档。<!DOCTYPE>声明必须在 HTML 文档的第一行，但这并不是一个 HTML 标签。

2. 严格模式和混合模式如何区分？他们有什么意思？

   标准(严格)模式的排版和js运作模式都是以该浏览器支持的最高标准运行。
   
   在兼容模式( 混合模式或怪异模式)中，页面以宽松的向后兼容的方式显示，模拟老式浏览器的行为以防止站点无法工作。




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





### 项目目录结构

![20191225163735830](https://s1.imagehub.cc/images/2024/11/03/d37c11b34ac01ce3cdb2d79bf6a36483.png)






### js符号优先级

| 优先级 | 运算符                                                       | 说明                                                   |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------ |
| 1      | []  .   ()                                                   | 字段访问、数组索引、函数调用和表达分组                 |
| 2      | ++  --   -   ~   !   delete new  typeof  void                | 一元运算符、返回数组索引、对象创建、未定义的值         | 
| 3      | *  /   %                                                     | 相乘、相除、求余数                                     | 
| 4      | +  -                                                         | 相加、相减、字符串拼接                                 | 
| 5      | <<   >>   >>>                                                | 左位移、右位移、无符号右移                             | 
| 6      | <    <=   >   >=   instanceof                                | 小于、小于或等于、大于、大于或等于、是否为特定类的实例 | 
| 7      | ==   !==   ===   !==                                         | 相等、不相等、全等、 不全等                            | 
| 8      | &                                                            | 按位‘与‘                                               | 
| 9      | ^                                                            | 按位‘异或’                                             | 
| 10     | \|                                                           | 按位'或'                                               | 
| 11     | &&                                                           | 短路与（逻辑 ’ 与 ‘）                                  | 
| 12     | \|\|                                                         | 短路或（短路 ’ 或 ‘）                                  | 
| 13     | ?:                                                           | 条件运算符                                             | 
| 14     | =   +=   -=   *=   /=   %=   &=   \|=   ^=   <   <=  >   >=   >>= | 混合赋值运算符                                      
| 15     | ，                                                           | 多个计算                                               | 



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





### src和href的区别

1. href标识超文本引用，用再link等元素上，href和a等元素上，href是引用和页面关联，实在当前元素和引用资源之间建立联系。
2. src表示引用资源，表示替换当前元素，用在img，script，iframe上，src是页面内容不可缺少的一部分。

3. src是指向外部资源的位置，指向的内部会迁入到文档中当前标签所在的位置；在请求src资源时会将其指向的资源下载并应用到当前文档中，列入js脚本，img图片和ifame等元素。



### Event loop

javaScript是单线程，所有任务都需要排队，前一个任务结束，才会执行后一个任务。

而这种**主线程从"任务队列"中读取执行事件，不断循环重复的过程**，就被称为**事件循环（Event Loop）**

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

### 可选链
  作用：可选链操作符(?.)允许读取位于链接对象链身处的属性的值    
  如果该链任意一环节不存在，则忽略整个链并返回undefined。  
  语法：  
  ```js
  obj?.prop
  obj?.[expr]
  func?.(args)
  ```



### new的执行过程

使用new关键字调用构造函数Student，分为四步。

1. 在内存中创建了一个实例对象（内容为空）

  ``var stu1={}``

2. 设置该实例对象的_ _proto_ _属性执行构造函数的prototype原型对象

   ``stu1.__proto__==student.protope``

3. 使用该实例对象stu1调用构造函数，改变构造函数中的this指向为实例对象stu1

   ``Student('张三'，20).call(stu1)``

4. 返回刚刚建好的实例对象



### JS常见的内存泄漏

1. 意外的全局变量（全局变量很难被垃圾回收器回收，所以会产生内存泄漏）
2. 被遗忘的计时器或回调函数（页面关闭，忘记清除定时器）
3. 脱离DOM的引用（dom成了变量，此时同样的dom元素存在两个引用)
4. 闭包

**内存泄漏的识别方法**

+ Chrome浏览器的控制台Performance或Memory
+ Node提供process.memoryUsage方法

**避免内存泄漏**

+ 注意程序逻辑，避免死循环
+ 减少不必要的全局变量或者相对作用域链上的全局变量或者生命周期很长的对象，及时回收
+ 避免频繁创建过多的对象，用完了记得销毁





### js浮点数运算精度问题

**产生原因：**
  
计算机底层会将十进制转为二进制。0.1和0.2转为二进制都会产生一个无限循环的数，计算机中是不允许无限循环的数，会进行舍入处理。双精度浮点数的小数部分最多支持52位，因浮点数小数位的限制而截断的二进制的数字，这时候，我们再把它转为十进制，就出现了误差。

**解决方案：**

+ 将结果四舍五入（toFixed）
+ 将浮点数转为整数再将结果除以扩大的倍数
+ 把浮点数转为字符串，模拟实际运算的过程



### 垃圾回收和内存泄漏

**内存泄漏：**不再用到的内存，没有及时释放。

**垃圾回收：**为了避免内存的泄漏，垃圾回收机制会定期找出那些不再用到的变量，然后释放其内存，

垃圾回收有两种方式 :标记清除（常用）、引用计数。

+ 标记清除
  当变量进入环境时，就将这个变量标记为"进入环境"，当变量离开环境时，则将其标记为“离开环境”，离开环境，自动被回收。

+ 引用计数
  语言引擎有一张“引用表”保存了内存里面所有资源的引用次数，如果一个值的引用次数为0，就表示这个值没有用到了，就会被内存释放。



### 前端数据加密方法

+ md5加密
+ base64加密
+ sha1加密
+ RSA加密



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


### npm、cnpm、yarn的区别
  1. npm: 网速慢。容易造成版本不统一。输出内容长。
  2. cnpm: 网速快。淘宝对npm的拷贝，10分钟同步一次。
  3. yarn: 以前安装过，后期可以离线安装。版本统一。扁平模式（将依赖包的不同版本归结为单个版本，以避免创建多个副本）


### js中if判断true和false
''、0、undefined、null、false、NaN都为false。其他的都为true。




### 复制数组的方法

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





## 详细事件

### addEventListener事件监听


鼠标事件

| 事件 |	触发 |  
| --------- | ------------------------ |   
| onclick |	点击时 |    
| ondblclick |	双击时 |
| onmousedown |	按下左键释放之前 |
| onmouseup |	在页面元素上移动鼠标 |
| onmouseout |	指针移出元素范围 |
| onmouseover |	第一次移入指定元素范围 |
| onmouseup |	释放按下的左键时发生 |
| ondrag |	元素被拖动时 |
| ondragstart |	在拖动操作开端运行 |
| ondragend |	拖动操作末端运行 |
| ondragenter |	当元素元素已被拖动到有效拖放区域时 |
| ondragleave |	当元素离开有效拖放目标时运行 |
| ondragover |	当元素在有效拖放目标上正在被拖动时 |

键盘事件        

| 事件 |	触发 |  
| --------- | ------------------------ |    
| onkeypress |	用户按下一键未释放时 |  
| onkeydown |	单击键盘时 |    
| onkeyup |	键盘按下再放开时发生 |  

表单事件    

| 事件 |	触发 |  
| --------- | ------------------------ |    
| onsubmit |	用户提交表单时发生 |    
| onchange |	在域的内容改变时发生 |  
| onreset |	表单数据被重置时发生 |  
| onselect |	用户从文本框中选择文本时发生 |  
| onfocus |	获得焦点时 |    
| onblur |	失去焦点时触发 |    

读取事件    

| 事件 |	触发 |  
| --------- | ------------------------ |    
| onload |	页面或图像加载完毕时触发 |    
| onunload |	用户离开页面时触发 |    
| onbeforeunload |	用户离开页面时触发 |    

文档事件  

| 事件 |	触发 |      
| --------- | ------------------------ |    
| onload |	页面或图像加载完毕时触发 |    
| onunload |	用户离开页面时触发 |    
| onbeforeunload |	用户离开页面时触发 |
| onabort |	用户停止浏览器继续下载图像时触发 |
| onerror |	当浏览器载入网页或图像发生错误时 |
| onload |	通常用于 body元素，在页面完全载入后触发(包括图片、css文件等等。) |
| onresize |	窗口或框架被调整大小时发生。 |
| onunload |	用户离开页面时发生 |    



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


### js的继承，优缺点

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


### HTTP协议状态码

浏览器与web服务器之间的通信协议  
2xx成功，3xx请求重定向，4xx客户端错误，5xx服务器错误。  

301-临时重定向  
302-永久重定向  
303-表示资源存在另一个URL，用GET方法获取资源  
304-本地缓存有资源，不需要重新请求  

400-(错误请求)服务器不理解请求的语法    
401-表示发送的请求需要有通过HTTP认证的认证信息  
403-(禁止，权限不够)服务器拒绝请求  
404-(未找到)服务器找不到请求网页  
405-参数错误，url错误，请求类型错误

500-内部服务器错误  

 

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

