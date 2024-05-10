## addEventListener事件监听


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



## Object中的方法

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




## Map和Set

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





## jQuery

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

