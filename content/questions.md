?> 其中很多题都是对于代码的深度思考，为什么要这么做？  
还有很多思路题，只需要提出解决思路即可。

### API接口安全对接
  API接口安全对接是指在不同系统之间进行数据交互时，确保接口的安全性和可靠性的一种方式。以下是API接口安全对接的一般步骤：
  + 身份验证：在进行API接口对接之前，需要进行身份验证，确保只有授权的用户或系统可以访问接口。常见的身份验证方式包括使用API密钥、令牌或证书等。
  + 数据加密：为了保护数据的机密性，可以使用加密算法对传输的数据进行加密，常见的加密算法包括AES、RSA等。
  + 防止重放攻击：为了防止恶意用户重复使用已经传输的请求，可以在请求中添加时间戳或随机数参数，并在服务端进行验证。
  + 参数检验：在接受到请求后，需要对请求参数进行验证，确保参数的合法性和完整性。可以使用正则表达式、数据格式验证等方式进行参数检验。
  + 接口访问控制：对于不同的接口，可以设置不同的访问权限，确保只有具备相应权限的用户或系统可以使用。
  + 日志记录与监控：对于接口的访问情况和异常情况，需要进行日志记录和监控，及时发现和处理异常情况。
  + 异常处理：在接口对接过程中，可以回出现各种异常情况，需要进行合理的异常处理，包括错误返回，异常信息记录等。

### 20分钟页面不操作，页面失效怎么实现
+ web worker使用setInterval（轮询）。
+ 前端记录用户最后操作时间（鼠标触发事件），用户下一次操作自动重新登录。
+ 后台接口检验，检查上一个接口和本次接口的时间间隔。

### 运行大量耗时并且会占用主线程的任务，保证页面不卡顿
 将所有耗时函数放入到requestAnimationFrame中，判断每次16.6毫秒就让页面更新，页面更新完后继续执行。
[视频地址](https://www.bilibili.com/video/BV1184y117Pj/?spm_id_from=333.337.search-card.all.click&vd_source=1f32a8797e6b69ce980a73da54121281)

### 漏洞防御

+ xss跨站脚本攻击（原理，如何进行的，防御手段是什么）
+ CSRF跨站请求伪造（如何防伪造，怎么防御，等等都要说清楚）
+ sql脚本注入（注入方式，防御方式） 
+ 上传漏洞（防御方式）

### 做过哪些组件封装

1. 工具函数的封装
   1. 获取时间的方法，时间相减。
   2. 对象扁平化。
   3. localStorage方法，存储对象。
   4. axios封装
      统一请求ip地址，baseURL
      请求拦截：添加时间戳，token
      响应拦截：根据code码进行判断。
2. 组件封装
   1. Echarts图表封装（自定义数据格式，大小自适应）
   2. Element表格封装

### git常见的冲突，如何解决
**冲突原因**
   1. 多个开发者修改相同文件下，同一行代码。
   2. 重命名、移动、删除文件时，其他分支也对该文件进行了修改。
**预防冲突**
   1. 及时更新代码
   2. 区分每个人的开发模块，避免开发到同一模块
   3. 频繁提交

### 二次封装 localStorage，需要考虑什么?
+ **注意命名，防止污染**    
   比如一个域名下有两个子项目，两个子项目中都要存储`userInfo`。为了防止数据互相污染，就**给对应的变量加上前缀**。

+ **注意版本，迭代防范**   
   项目更新之前`userInfo`用来存的字符串，更新后存的对象，存取方式不一样，容易报错。每次更改内容，可以**添加一个版本号**

+ **时效性**    
   存数据时，加入一个时间戳，取数据时做判断

+  **兼容 SSR（服务端渲染）**   
   在服务端是使用不了 localStorage 的，因为不是浏览器环境，所以你像封装一个比较通用的 localStorage，得兼顾 SSR 的情况

+ **加密**

+ **存入取出类型转换（注意考虑map、set、Date类型）**  
   使用`instanceof`判断类型，存入的时候添加类型，取出的时候根据类型判断。

<details> 
   <summary>点我展开看代码</summary>

   ```js
      class EnhancedLocalStorage {  
         static serialize(value) {  
            if (value instanceof Map) {  
                  return JSON.stringify({  
                     type: 'Map',  
                     value: Array.from(value.entries())  
                  });  
            } else if (value instanceof Set) {  
                  return JSON.stringify({  
                     type: 'Set',  
                     value: Array.from(value.values())  
                  });  
            } else if (value instanceof Date) {  
                  return JSON.stringify({  
                     type: 'Date',  
                     value: value.toISOString()  
                  });  
            } else if (typeof value === 'object' && value !== null) {  
                  return JSON.stringify(value);  
            } else {  
                  return value;  
            }  
         }  
      
         static deserialize(value) {  
            if (typeof value !== 'string') {  
                  return value;  
            }  
      
            const parsed = JSON.parse(value);  
      
            if (parsed.type === 'Map') {  
                  return new Map(parsed.value);  
            } else if (parsed.type === 'Set') {  
                  return new Set(parsed.value);  
            } else if (parsed.type === 'Date') {  
                  return new Date(parsed.value);  
            } else {  
                  return parsed;  
            }  
         }  
      
         setItem(key, value) {  
            const serializedValue = EnhancedLocalStorage.serialize(value);  
            localStorage.setItem(key, serializedValue);  
         }  
      
         getItem(key) {  
            const serializedValue = localStorage.getItem(key);  
            return EnhancedLocalStorage.deserialize(serializedValue);  
         }  
      
         removeItem(key) {  
            localStorage.removeItem(key);  
         }  
      
         clear() {  
            localStorage.clear();  
         }  
      
         // Optional: Add methods to handle keys, e.g., getAllKeys()  
         getAllKeys() {  
            return Array.from(localStorage.keys());  
         }  
      }  
      
      // Usage example:  
      const storage = new EnhancedLocalStorage();  
      
      // Store various types of data  
      const myMap = new Map([['key1', 'value1'], ['key2', 'value2']]);  
      const mySet = new Set([1, 2, 3]);  
      const myObject = { name: 'Alice', age: 25 };  
      const myDate = new Date();  
      
      storage.setItem('myMap', myMap);  
      storage.setItem('mySet', mySet);  
      storage.setItem('myObject', myObject);  
      storage.setItem('myDate', myDate);  
      
      // Retrieve and verify the data  
      console.log(storage.getItem('myMap')); // Map { 'key1' => 'value1', 'key2' => 'value2' }  
      console.log(storage.getItem('mySet')); // Set { 1, 2, 3 }  
      console.log(storage.getItem('myObject')); // { name: 'Alice', age: 25 }  
      console.log(storage.getItem('myDate')); // Date object representing the same date and time as myDate
      
   ```
</details>


```js

//下面代码输出的结果是什么
const obj={
   a:0
};
obj['1'] = 0;
obj[++obj.a] = obj.a++;
const values = object.values(obj);
obj[values[1]] = obj.a
console.log(obj);

```

### forEach和map跳出循环
  ```js
    // 采用try..catch.. 和  throw new Error()来实现条件跳出，或者报错防止阻塞代码的作用
  // 1. 单层循环：
  try{
    obj.forEach(item => {
      console.log(`当前id：${item.id}`)
      if(item.id === '002'){
        throw new Error('id等于002，跳出循环');
      }
    });
  }
  catch(error){
    console.error(error)
  };
  console.log("如果看见了这段话说明代码没有被报错所阻塞");

  // 2. 双层循环：
  // 只是跳出了第二层循环，第一层循环会继续执行的

  try{
    obj.forEach(item => {
      console.log(`第一层forEach循环：${item.id}`);
      try{
        item.array.forEach(val => {
          if(val.age < 18){
            throw  new Error('年龄不能小于18岁');
          }
        })
      }catch(error){
        console.error(error)
      }
    })
  }catch(error){
    console.log(error)
  };
  console.log("如果看见了这段话说明代码没有被报错所阻塞");
  ```

### CSS 动画和 JavaScript 动画的优缺点
#### css动画
优点：   
 + 硬件加速：CSS 动画会使⽤浏览器的 GPU 来进⾏硬件加速，能够更加流畅和⾼效地运⾏。 
 + 简单易⽤：CSS 动画通常只需要⼏⾏代码就能实现基本的动画效果，不需要使⽤ JavaScript 来控制动画。 
 + 低资源占⽤：CSS 动画通常⽐ JavaScript 动画使⽤更少的 CPU 和内存资源，因此更适合⽤于简单的动画效果。  

缺点：   
 + 限制较⼤：CSS 动画在实现复杂的动画效果时，受到限制较⼤，不能像 JavaScript 动画那样⾃由控制动画的速度、⽅向等。
 + 兼容性问题：由于不同浏览器对 CSS 动画⽀持程度不同，因此在实现时需要考虑浏览器兼容性问题。
 + 可维护性差：当动画效果较为复杂时，使⽤ CSS 实现的代码会变得冗⻓和难以维护，因此需要进⾏代码优化和结构设计。
 + 缺乏交互性：CSS动画通常只能在元素加载时播放一次，不能根据用户行为进行交互。

#### JavaScript 动画
优点：  
 + ⾃由控制：JavaScript 动画能够更加⾃由地控制动画的速度、⽅向等，可以实现更加复杂的动画效果。  
 + 兼容性好：由于 JavaScript 是浏览器通⽤的语⾔，因此在实现动画效果时，能够更好地兼容不同的浏览器。   
 + 可维护性强：使⽤ JavaScript 实现动画时，代码结构更加灵活，能够更好地维护和扩展。 

缺点：   
 + 资源占⽤⾼：JavaScript 动画通常需要更多的 CPU 和内存资源，因此在实现动画效果时需要考虑系统资源的消耗问题。  
 + 性能问题：JavaScript 动画性能受 JavaScript 引擎的影响，⽽不是浏览器引擎，因此需要对代码进⾏优化以提⾼动画性能。   
 + 复杂度⾼：JavaScript 动画的实现复杂度通常⽐ CSS 动画⾼，因此需要对动画效果进⾏设计和规划。   

### 什么是 FOUC (无样式内容闪烁)?你如何来避免 FOUC?
FOUC（Flash of Unstyled Content，无样式内容闪烁）是指在网页加载过程中，用户可能会短暂地看到未应用样式的原始HTML内容，随后样式表加载完成后，页面才会以正确的样式重新渲染。这种现象会影响用户体验，显得页面加载不连贯和不专业。FOUC通常是由于样式表加载延迟或顺序不当引起的，具体原因可能包括：

+ 样式表放在HTML文档的底部，或通过JavaScript动态加载。
+ 外部样式表通过外部链接引用，加载速度依赖于网络连接状况。
+ 使用JavaScript动态修改样式或内容，导致内容在JavaScript执行前短暂无样式。
+ Web字体加载也可能导致FOUC。

为了避免FOUC，可以采取以下措施：

1. 确保样式表链接位置正确：将样式表链接放在HTML文档的`<head>`部分，确保在页面渲染之前先加载样式。
2. 使用内联CSS：将CSS样式直接嵌入到HTML文档头部，这样也可以确保在页面渲染之前先加载样式。
3. 预加载样式表：使用`<link rel="preload">`标签来预加载CSS文件，确保在渲染阶段之前提前加载样式。
4. 优化外部字体加载：使用font-display: swap或其他字体加载策略，确保在字体加载期间使用后备字体，避免内容无样式闪烁。
5. 避免阻塞脚本：确保JavaScript脚本不会阻塞CSS样式的加载，可以使用async或defer属性来异步加载脚本。
6. 使用样式回退：在CSS样式加载之前，可以使用基本的HTML样式来避免FOUC，确保页面在加载完成前依然有可用的样式。
7. 使用样式表框架：一些流行的样式表框架（如Bootstrap或Foundation等）已经对FOUC问题进行了优化和处理，使用这些框架也可以降低FOUC的发生概率。

### 为什么说“避免使用内联事件处理器”是好的实践？
1. 代码重复难以维护
2. 可读性差
3. 难以调试
4. 不利于代码重用
5. 安全性问题

### 你能描述渐进增强 (progressive enhancement) 和优雅降级 (graceful degradation) 之间的不同吗?
**渐进增强：**针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。（从被所有浏览器支持的基本功能开始，逐步地添加那些只有新式浏览器才支持的功能，向页面添加无害于基础浏览器的额外样式和功能。当浏览器支持时，它们会自动地呈现出来并发挥作用。）

**优雅降级：**一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。（Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会检查以确认它们是否能正常工作。由于IE独特的盒模型布局问题，针对不同版本的IE的hack实践过优雅降级了，为那些无法支持功能的浏览器增加候选方案，使之在旧式浏览器上以某种形式降级体验却不至于完全失效。）

**区别：**优雅降级是从复杂的现状开始，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的、能够起作用的版本开始，并不断扩充，以适应未来环境的需要。

### 假若你有 5 个不同的样式文件 (stylesheets), 整合进网站的最好方式是?

根据class命名规则写样式。提取公共的样式，进行合并，非公共的单独拎出来。然后打包压缩一下就行了，若每个文件都很大，就需要分模块加载。

### 你能描述当你制作一个网页的工作流程吗?

1. 内容分析：分清展现在网络中内容的层次和逻辑关系
2. 结构设计：写出合理的html结构代码
3. 布局设计：使用html+css进行布局
4. 样式设计：首先要使用reset.css
5. 交互设计：鼠标特效
6. 行为设计：js代码，ajax页面行为和从服务器获取数据
7. 测试兼容性；优化性能。

### 浏览器标准模式和怪异模式之间的区别是什么？

W3C标准推出以后，浏览器都开始采纳新标准，但存在一个问题就是如何保证旧的网页还能继续浏览，在标准出来以前，很多页面都是根据旧的渲染方法编写的，如果用的标准来渲染，将导致页面显示异常。为保持浏览器渲染的兼容性，使以前的页面能够正常浏览，浏览器都保留了旧的渲染方法（如：微软的IE）。这样浏览器渲染上就产生了Quircks mode和Standars mode，两种渲染方法共存在一个浏览器上。IE盒子模型和标准W3C盒子模型：ie的width包括：padding\border。标准的width不包括：padding\border。  

在js中如何判断当前浏览器正在以何种方式解析？

document对象有个属性compatMode,它有两个值：BackCompat对应quirks mode CSS1Compat对应strict mode。


### 解释一下CSS中的“级联”规则是什么，以及它是如何工作的？
[内容详情](https://www.zhangxinxu.com/wordpress/2022/05/deep-in-css-cascade/)

   <details> 
      <summary>点我展开详情</summary>

#### （一）简述

CSS中有两个重要的基础规则，一个是级联（Cascading），一个是继承（Inheritance）。     
继承指的是类似 color, font-family, visibility 等属性父元素设置，子元素会被继承的特性。    
那级联指的是什么呢？    
在 JS 中，方法的连续执行可以称为级联。    
例如：   
   ```js
      var fn = {
      a: function () {
         return this;
      },
      b: function () {
         return this;
      }
      };
      // 级联调用
      fn.a().b();
   ```
   CSS中的级联与上面神似。 
   当我们应用某个 CSS 样式的时候，你可以理解为有很多的前后应用方法。 
   ```js
      fn.styleA().styleB().styleC()...
   ```
   最终该应用哪个 CSS 样式，就是基于这些级联规则来的。
   按照目前的 CSS 规范的描述，CSS 级联的优先级是这样的（按序号递减）：
   1. transition 过渡声明；
   2. 设置了 !important 的浏览器内置样式；
   3. 设置了 !important 的用户设置的样式；
   4. 前端开发者在 @layer 规则中设置的包含 !important 的样式；
   5. 前端开发者平常设置的包含 !important的样式；
   6. animation 动画声明；
   7. 前端开发者设置的 CSS 样式。
   8. @layer 规则中的样式；
   9. 用户在浏览器中设置的样式；
   10. 浏览器自身内置的样式；

   #### （二）级联规则详解
   1. 先不用管 !important        
   为了方便我们理解，我们可以先不用关心 !important 对级联优先级的影响。  
   因此，理论上的级联优先级是：  
   transition > animation > 常规CSS > @layer规则 > 用户设置 > 浏览器内置  
   2. 也不用管 transition 和 animation   
   transition 和 animation 声明下的级联规则大家也可以不用太关心，为什么呢？  
   主要是浏览器的真实表现和规范中定义的并不一样。  
   例如设置了 !important 属性的 CSS 应该优先级比 animation 高，但是，在 IE，IE Edge，Chrome 以及 Safari 浏览器下，动画执行的优先级是最高的，超越 !important。
   《CSS新世界》中有专门介绍过，[demo见这里](https://demo.cssworld.cn/new/5/4-1.php)。
   CSS新世界中的animation优先级
   至于 transition 的最高优先级更是无从谈起，我反复测试，都是普通 CSS 属性的表现。
   所以，我们应该关心的级联优先级其实就这么几个：
   `常规CSS > @layer规则 > 用户设置 > 浏览器内置`
   3. 常见且重要的四种级联规则
   常规CSS   
   所谓常规 CSS，指的是开发人员在 CSS 文件，`<style>` 元素，或使用 `HTML style` 内联属性设置的 CSS样式。
   开发者 CSS 代码示意
   `@layer规则`
   CSS @layer 规则是最近现代浏览器纷纷支持了一个极具颠覆性的新特性，兼容性如下图所示：
   @layer 规则兼容性
   这个规则可以让其中设置的所有 CSS 的优先级降低，特别适合在引入某个模块的时候使用，可以优先避免他人的代码因为优先级原因影响自己的代码。
   例如：
   ```js
      <button id="button">我是按钮</button>
      button {
         color: red;
      }
      @layer {
         #button {
            color: green;
         }
      }
   ```
   此时虽然 ID 选择器的优先级很高，但由于在 @layer 规则中，优先级没有外面的标签选择器 button 高，因此按钮是红色：
   layer 简单示意
   关于 @layer 规则我会在下一篇文章中详细介绍。
   用户设置
   用户设置的 CSS 多指用户安装插件等工具所设置的 CSS（称为“注入的样式表”），比方说 Adblock 等插件对页面元素隐藏的 CSS 就属于这一类。
   以及，我个人认为（实际并不准确），用户通过浏览器自身的设置改变浏览器的主题背景，字号或字体等也可以归为这一类。
   浏览器的设置
   浏览器内置
   官方说法叫做用户代理样式，其实就是浏览器内置的样式。
   这个大家都见得比较多，很多 HTML 元素会内置样式，常见的如 `<body>`, `<p>` 等元素的 margin 外间距，`<input>`、`<button>`等元素的边框和背景色样式等。
   用户代理样式表
   上面这四种类型就是目前主要的级联规则。
   每一种级联规则的优先级都是超越下一个级联规则的，除非使用 !important 进行逆袭，否则是无法重置。
   4. 逆向运作的 important 标识符
   !important 有个很有意思的特性，那就是原本级联水平高的CSS声明应用了!important后，其优先级反而低，而原本级联水平低的 CSS 声明应用了 !important 后，CSS 计算的优先级反而高。
   例如，用户代理 CSS（浏览器内置 CSS）在级联规则中处于底层，但是，一旦这些属性值的后面增加了 !important。
   不得了！绝地大翻身，超级大逆袭，优先级直接升到超级霸主的地位，完全不可撼动！
   如果我们平时比较敏感，就会看到浏览器内置的不少 CSS 后面设置了 !important。
   跟大家讲，这些 CSS 样式你就不要白日做梦，说的是我去重置他！
   瞎子点灯白费蜡，一点毛用都没有！
   无法重置的 CSS 
   同样的，Chrome 有很多广告拦截插件，其会通过注入 CSS 的方式让广告容器隐藏，其相关代码会是这样的：
   注入的样式表示意
   这些里的 display: none 隐藏开发人员是无论如何也无法重置的，被级联规则给限制了。
   三、完整的样式优先级
   一个 CSS 样式是否生效，其优先级是由下面这三句话决定的。
   这三句话很重要，大家可以拿小本本记一下。
   1. 继承是最底层，低于所有的级联规则。
   2. 级联规则无法跨越，除非使用 !important 逆袭。
   3. 同一级联规则内的优先级按照选择器权重和先后顺序决定。
   用一张图表示就是：
   优先级示意

   </details>

### js的垃圾回收基础，有什么问题，如何优化
[详细](https://blog.csdn.net/lph159/article/details/142207529)

#### 一、垃圾回收机制概述
1. 什么是垃圾回收？
在编程语言中，内存管理是一个非常重要的方面。JavaScript 作为一种高级语言，开发者不需要手动管理内存的分配和释放。垃圾回收机制是 JavaScript 引擎中的一部分，负责自动回收那些不再被使用的内存，确保内存资源得到有效利用，避免内存泄漏。

简单来说，当程序中某些对象不再被引用时，这些对象所占用的内存就会被视为“垃圾”，垃圾回收器会负责释放这些内存，使其可以被重新利用。

2. 为什么需要垃圾回收？
由于 JavaScript 是动态分配内存的语言，当创建变量、对象、函数等时，都会占用一定的内存。如果这些占用的内存长期不被释放，就会造成内存泄漏，最终可能导致程序崩溃或性能问题。因此，垃圾回收的核心作用就是自动检测不再使用的内存并释放它们，以保持程序的高效运行。

#### 二、JavaScript 的垃圾回收算法
JavaScript 的垃圾回收机制主要基于“引用计数”和“标记-清除”两种算法。接下来，我们将逐一详细介绍这些算法的工作原理。

1. 引用计数算法

1.1 工作原理
引用计数（Reference Counting）是最简单的一种垃圾回收算法。它的基本原理是：每个对象都有一个引用计数器，当有一个引用指向该对象时，计数器加 1；当一个引用不再指向该对象时，计数器减 1。如果某个对象的引用计数变为 0，则表示该对象不再被任何地方引用，可以安全地释放。

 1.2 示例
 ```js
let obj1 = { name: 'Alice' }; // obj1 的引用计数为 1
let obj2 = obj1; // obj1 的引用计数为 2
obj1 = null; // obj1 的引用计数为 1
obj2 = null; // obj1 的引用计数为 0，此时对象可以被垃圾回收
```
 1.3 缺陷
虽然引用计数算法很直观，但它有一个明显的缺陷——循环引用。如果两个对象互相引用，即使它们不再被其他对象引用，它们的引用计数也不会归零，导致内存无法被释放。
 ```js
function createCycle() {
    let obj1 = {};
    let obj2 = {};
    obj1.ref = obj2; // obj1 引用 obj2
    obj2.ref = obj1; // obj2 引用 obj1
    return obj1;
}
createCycle();
```

在上述代码中，obj1 和 obj2 互相引用，导致它们的引用计数永远不会归零，从而无法被垃圾回收。这种情况称为内存泄漏。

2. 标记-清除算法

2.1 工作原理      
为了克服引用计数算法的缺陷，大多数现代 JavaScript 引擎使用的是标记-清除（Mark-and-Sweep）算法。这种算法的工作流程如下：

标记阶段：垃圾回收器从根对象（通常是全局对象或局部作用域的变量）开始，递归地标记所有可以被引用到的对象为“活动对象”。
清除阶段：对于那些没有被标记为“活动”的对象，它们被认为是不可达的，垃圾回收器会释放它们所占用的内存。

2.2 示例  
 ```js
let obj1 = { name: 'Alice' };
let obj2 = { name: 'Bob' };
let obj3 = { name: 'Charlie' };

obj1.friend = obj2; // obj1 引用 obj2
obj2.friend = obj3; // obj2 引用 obj3
obj1 = null; // 断开 obj1 的引用
```

在这个例子中，obj1 被置为 null 后，obj2 和 obj3 仍然被引用，因此它们不会被回收。然而，假如 obj2 和 obj3 的引用也被断开，它们将被标记为不可达对象，最终会在清除阶段被回收。

3. 增量垃圾回收和分代回收
为了提高垃圾回收的效率，现代 JavaScript 引擎（如 V8）引入了更复杂的回收机制，如增量垃圾回收和分代回收。

3.1 增量垃圾回收
标记-清除算法虽然有效，但在处理大量对象时可能会导致应用程序卡顿。为了解决这个问题，V8 引擎采用了增量垃圾回收，即将垃圾回收的工作分成多个小步骤，分散在程序的执行过程中。这样可以避免长时间的卡顿，提升用户体验。

3.2 分代回收
分代回收的思想是将内存分为两代：新生代和老生代。新创建的对象被放置在新生代中，如果这些对象能够长期存活，则被移动到老生代。垃圾回收器会更加频繁地清理新生代中的对象，而老生代的对象因为生命周期较长，则不需要频繁清理。这种方式大大提高了垃圾回收的效率。

#### 三、垃圾回收中的内存泄漏问题
虽然 JavaScript 的垃圾回收机制极大地简化了内存管理，但某些情况下，内存泄漏仍然是开发者需要注意的问题。

1. 常见的内存泄漏场景

1.1 未清理的事件监听器
当你为 DOM 元素添加事件监听器时，如果不在适当的时机移除监听器，可能会导致内存泄漏。
 ```js
let button = document.getElementById('myButton');
button.addEventListener('click', function() {
    console.log('Button clicked!');
});
// 记得在不再需要时移除事件监听器
button.removeEventListener('click', listenerFunction);
```
1.2 闭包引发的内存泄漏
闭包可以保留对其外部变量的引用，如果这些引用不被适时释放，也会导致内存泄漏。
 ```js
function createClosure() {
    let bigArray = new Array(10000).fill(0);
    return function() {
        console.log(bigArray.length);
    };
}
let closure = createClosure();
```
在上面的例子中，虽然 bigArray 已经不再需要，但由于闭包的存在，它的内存不会被回收，除非 closure 本身也被释放。

1.3 DOM 元素的循环引用
在某些情况下，JavaScript 对象和 DOM 元素之间的循环引用可能会阻止垃圾回收。例如，JavaScript 对象持有 DOM 元素的引用，而 DOM 元素的属性也引用了 JavaScript 对象。

#### 四、如何优化垃圾回收
1. 避免全局变量
全局变量在程序的整个生命周期中都不会被回收，因此尽量避免使用全局变量，或在不再需要时将其设置为 null。

2. 合理使用闭包
虽然闭包是 JavaScript 中强大的功能，但应避免不必要地持有对外部变量的引用，以减少内存泄漏的风险。

3. 使用弱引用
JavaScript 提供了 WeakMap 和 WeakSet，它们不会阻止垃圾回收。使用这些数据结构可以减少内存泄漏的可能性。



### ECMAScript和JavaScript的关系

ECMAScript和JavaScript之间的关系是标准与实现的关系。
JavaScript最初是由Netscape公司（现为Mozilla基金会的一部分）开发的一种脚本语言，用于为网页添加动态功能。随着互联网的发展，JavaScript逐渐成为了网页开发不可或缺的一部分。

为了标准化JavaScript并确保不同浏览器之间的兼容性，欧洲计算机制造商协会（ECMA，后更名为ECMA International）在1996年成立了一个委员会，专门负责制定JavaScript语言的规范。这个规范被称为ECMAScript。因此，ECMAScript实际上是JavaScript语言的标准规范，定义了该语言的语法、数据类型、操作符、对象等核心组成部分。

简而言之，ECMAScript是JavaScript的标准，而JavaScript是ECMAScript标准的具体实现之一。尽管在实际开发中，我们通常将ECMAScript和JavaScript视为同义词，但严格来说，它们之间还是存在细微的差别的。当我们谈论JavaScript时，我们可能指的是这门语言本身、它的各种实现（如浏览器中的JavaScript引擎）、以及与之相关的API（如DOM和BOM）等。而当我们谈论ECMAScript时，我们更侧重于指这门语言的语法和语义规范。

随着Web技术的不断发展，ECMAScript标准也在不断更新和完善。从ECMAScript 3（1999年发布）到最新的ECMAScript 2023（也称为ES14），每个新版本都引入了一些新特性和改进，旨在使JavaScript更加现代化、高效和易于使用。


ECMAScript和JavaScript之间的关系：
<details> 
   <summary>比喻</summary>

比喻：     
想象你是一位厨师（开发者），你正在准备一顿美味的饭菜（编写JavaScript代码）。你的厨房（浏览器）是你进行烹饪（代码执行）的地方，它提供了你所需的所有工具和设备（如炉灶、烤箱、刀具等，对应浏览器的各种功能和API）。      

现在，假设你所在的地区（Web开发社区）有一个烹饪协会（ECMA International），它负责制定烹饪规范（JavaScript规范，特别是ECMAScript）。这些规范告诉你如何正确地准备食材（编写代码），包括使用哪些烹饪技巧（语法和语义），以及如何将不同的食材组合在一起（函数、对象等）。     

每当烹饪协会发布新的烹饪规范时（ECMAScript更新版本），它可能会引入新的烹饪技巧或食材（新的JavaScript特性）。然而，这并不意味着你的厨房（浏览器）会立即拥有这些新的工具或食材。     

实际情况：    

浏览器更新：为了支持新的烹饪规范（ECMAScript版本），你的厨房（浏览器）需要进行升级或改造。这通常意味着浏览器开发商需要添加新的功能或改进现有功能，以确保它们能够按照新的规范来烹饪（执行JavaScript代码）。
兼容性：不是所有的厨房（浏览器）都会立即进行升级。有些厨房可能由于各种原因（如资源限制、旧设备的兼容性等）而延迟升级。因此，即使烹饪协会发布了新的规范，也可能会有一些厨房（浏览器）暂时无法支持这些新特性。
开发者责任：作为厨师（开发者），你需要了解你的目标顾客（用户）所使用的厨房（浏览器）类型，并相应地调整你的烹饪方法（编写代码）。如果某些顾客使用的是旧厨房（旧浏览器），你可能需要使用一些技巧（如代码转换工具Babel）来确保你的饭菜（代码）能够在他们的厨房中正确烹饪（执行）。
通过这个比喻，希望能够帮助你更好地理解浏览器、JavaScript规范（ECMAScript）以及它们之间的关系。简而言之，浏览器是JavaScript代码的运行环境，而ECMAScript规范定义了JavaScript代码的编写方式。每当ECMAScript更新版本时，浏览器需要相应地更新以支持这些新特性，但并非所有浏览器都会立即进行更新。
</details> 

### sass 和 less的区别

   #### 一、编译环境不同?
   less是通过js编译   在客户端处理
   sass是通过ruby编译 是在服务器端处理

   #### 二、变量符不一样
   less是使用@，sass是使用 $

   #### 三、使用方法
   sass支持条件语句，可以使用if{}else{},for{}循环等等。而less不支持。

   #### 四、输出设置

   less没有输出设置，sass提供4中输出选项：nested, compact, compressed 和 expanded。

   输出样式的风格可以有四种选择，默认为nested

   nested：嵌套缩进的css代码

   expanded：展开的多行css代码

   compact：简洁格式的css代码

   compressed：压缩后的css代码

   #### 五、Sass和Less的工具库不同

   （1）Sass有工具库Compass, 简单说，Sass和Compass的关系类似于像Javascript和jQuery的关系,Compass在Sass的基础上，封装了一系列有用的模块和模板，补充强化了Sass的功能。

   （2）Less有UI组件库Bootstrap,Bootstrap是web前端开发中一个比较有名的前端UI组件库，Bootstrap的样式文件部分源码就是采用Less语法编写。

   #### 六、Scss
   （1）含义：
   Sass 是采用 Ruby 语言编写的一款 CSS 预处理语言，它诞生于2007年，是最大的成熟的 CSS 预处理语言。最初它是为了配合 HAML（一种缩进式 HTML 预编译器）而设计的，因此有着和 HTML 一样的缩进式风格。Sass 和 SCSS 其实是同一种东西，我们平时都称之为 Sass，两者之间不同之处有以下两点：

   （A）文件扩展名不同。   
   Sass 是以“.sass”后缀为扩展名，而 SCSS 是以“.scss”后缀为扩展名。   
   （B）语法书写方式不同。 
   Sass 是以严格的缩进式语法规则来书写，不带大括号( { } )和分号( ; )，而 SCSS 的语法书写和我们的 CSS 语法书写方式非常类似。   
   （2）规则： 

   (a) 混合宏（@mixin声明，@include调用），类似于函数，可以传值或者直接调用。    
   (b) 扩展/继承（@extend来继承已存在的类样式块，将重复使用的样式延伸 (extend) 给需要包含这个样式的特殊样式。）   
   (c) 占位符 % placeholder：代码没有被 @extend 调用，他并没有产生任何代码块，编译出来的代码会将相同的代码合并在一起。与常用的 id 与class选择器写法相似，只是 # 或 . 替换成了 %。必须通过 @extend 指令调用。选择器占位符 %placeholder 有所限制，他不能在不同@media中运行。）  
   (d) @use：通过 @use  加载的模块不管被引用了多少次，都只会在编译后输出一次到 css 中。但是使用  @import  多次引入同一模块，会反复输出到 css 中。  
   (e) @forward：从其他Sass样式表加载mixin，function和变量，并将来自多个样式表的CSS组合在一起。    
   (f) @layer ：用于模块化组织样式,避免全局污染。     
   (g) @function：自定义函数，需要调用 @return 输出结果。并能在任何属性值或 Sass script 中使用。   
   (h) @content：在样式规则中插入外部内容，也就是说允许我们在@include时添加自定义样式到mixin中。   
   (i) @error：用于抛出错误,编译会在此终止。当某些条件不满足时,可以用@error抛出错误。  
   (j) @warn：输出一些警告或提示信息,编译不会终止。   
   (k) @debug：@debug用于输出调试信息,编译不会终止，可以打印变量值或语句来调试SCSS。   
   (l) @at-root：用于将样式放在根层级,破坏当前的嵌套规则。在需要跳出嵌套导致的重复选择器时使用。   

 ### 前端换肤方案
1. 硬编码。写多套css。
2. sass变量配置。
3. css属性。滤镜filter
4. 第三方库：Ant Design、Element UI等  


### 前端工程化

前端工程化是一种将前端开发流程系统化、规范化和自动化的方法，旨在提高前端开发的效率、可维护性和可扩展性。它涵盖了许多方面，包括项目结构、代码质量、自动化工具、性能优化等，以确保前端开发团队能够更高效地协作和交付高质量的前端应用程序。

以下是前端工程化的一些关键概念和实践：    
**项目结构：** 定义清晰的项目目录结构，使开发人员能够轻松查找和组织代码、样式和资源文件。   
**版本控制：** 使用版本控制系统（如Git）来跟踪和管理代码的变化，以便多个开发人员可以协同工作，并轻松回滚到以前的版本。   
**自动化构建：** 使用构建工具（如Webpack、Grunt、Gulp等）来自动化任务，如代码编译、压缩、打包和资源优化，以减少手动工作和减小文件大小。   
**模块化开发：** 采用模块化的代码结构，使开发人员能够更好地管理和复用代码，提高可维护性。   
**包管理器：** 使用包管理工具（如npm、Yarn）来管理和安装项目依赖，确保开发环境的一致性。   
**代码质量：** 引入代码风格检查工具（如ESLint、TSLint）和单元测试框架，以确保代码质量和可靠性。   
**自动化部署：** 使用持续集成/持续部署（CI/CD）工具来自动化应用程序的部署和发布过程，以确保快速且可靠的交付。   
**性能优化：** 优化前端性能，包括加载时间、资源压缩、懒加载等，以提供更好的用户体验。   
**文档和注释：** 编写清晰的文档和代码注释，以便其他开发人员能够理解和使用你的代码。  

前端工程化的目标是使前端开发更高效、更可靠，并促使开发团队采用一致的最佳实践。它在现代Web开发中变得至关重要，特别是在大型和复杂的项目中，可以显著提高开发团队的生产力和代码质量。


### 在制作一个网页应用或网站的过程中，你是如何考虑其 UI、安全性、高性能、SEO、可维护性以及技术因素的?

   #### 一、UI 
   界面美观，要有个性，考虑用户使用的逻辑要简单，用起来舒适自由。使用习惯要符合大部分用户的习惯，比如少让用户输入，采用选择的方式，提供搜索和提示功能。

   #### 二、安全性：
   1、对输入进行有效性验证（非法字符，特殊字符）如PHP中的方法htmlspecialchars()将特殊字符（>）转化为html实体，trim()去掉用户输入的不必要字符，stripslashes()去掉用户输入的反斜杠等等。      
   2、对交互操作进行身份验证和授权     
   3、异常错误处理（向用户反馈单额错误提示不要让攻击者分析出一些网络环境和配置）    
   4、缓冲区溢出；      
   5、注入攻击:注入攻击是应用违背了“数据与代码分离原则”导致的结果。它有两个条件：一是用户能够控制数据的输入；二是代码拼凑了用户输入的数据，把数据当作代码执行了。    
   6、不安全的存储；不要使用单独类似MD5或SHA加密策略，在进行散列密码值时，使用作料或多种作料以防止彩虹攻击。对于短密码，采 用一个短散列算法处理，例如：bcrypt或scrypt。    

   ####  三、高性能：

   1、DNS（域名系统）负载均衡；在DNS中为多个IP地址配置同一个域名如：`www.baidu.com`，因而查询这个域名的客户机将得到其中一个地址，从而使得不同的客户访问不同的服务器，达到负载均衡的目的，从而减小服务器端的压力。DNS负载均衡是一种简单而有效的方法，但是它不能区分服务器的差异，也不能反映服务器的当前运行状态。    
   2、HTTP重定向（通过使客户端重定向，来分散和转移请求压力，比如一些下载服务通常都有几个镜像服务器）；301重定向是网址重定向最为可行的一种办法,seo最为友好。    
   3、分布式缓存；      
   4、数据库扩展：读写分离，垂直分区，水平分区     
   5、反向代理负载均衡：让代理服务器将请求均匀转发给多台内部Web服务器之一上,从而达到负载均衡的目的。这种代理方式与普通的代理方式有所不同,标准代理方式是客户使用代理访问多个外部Web 服务器,而这种代理方式是多个客户使用它访问内部Web服务器,因此也被称为反向代理模式。

   使用反向代理的好处是,可以将负载均衡和代理服务器的高速缓存技术结合在一起,提供有益的性能,具备额外的安全性,外部客户不能直接访问真实的服务器。并且实现起来可以实现较好的负载均衡策略,将负载可以非常均衡的分给内部服务器,不会出现负载集中到某个服务器的偶然现象。

   ####  四、SEO:

   选好关键字，描述语言，修饰性图片换成文本，合理使用h1-h6，对图片添加alt属性，链接添加target属性。

   ####  五、可维护性：

   代码是否容易被理解，是否容易被修改和增加新的功能，当出现问题时是否能快速定位到问题代码。

### 虚拟列表的缺点
首先是一些问题        

1. 复杂性：实现虚拟列表需要进行更多的编程工作和逻辑处理。开发人员需要处理滚动和可见区域变化时的数据加载、渲染和更新等任务。
2. 难以处理动态列表：对于动态列表，即经常发生插入、删除或顺序变动的列表，虚拟列表可能更加复杂。因为它需要在可见区域发生变化时重新计算并更新列表项的位置。
3. 对于列表中列表项的高度不固定的情况需要一定的处理逻辑。
4. 随机访问开销：虚拟列表适用于大型列表的渲染和滚动，但如果用户需要随机访问列表中的项，而不仅限于顺序访问，虚拟列表就无法提供性能优势了。因为它需要在用户访问不可见的列表项时进行加载和渲染。
5. 预估和调优成本：正确实现虚拟列表需要合理地预估每个列表项的高度或大小，以便正确地计算和管理可见区域。这可能需要进行一些调试和优化，以确保虚拟列表的性能和可靠性。     
 需要注意的是，虚拟列表并非适用于所有情况，应根据具体需求和应用场景来评估其使用的适当性。有时，对于较小的列表或对性能要求不高的应用，使用虚拟列表可能并不必要。      

解决思路       
1. 对于经常发生插入、删除或顺序变动的列表，列表总数发生变化时，执行一些对应处理函数
2. 列表项的高度不固定的情况需要在dom初次渲染和更新的时候缓存数据里面更新列表项具体的位置和高度
3. 对于随机跳转到具体数据位置，可以先查找有没有该dom元素，没有就通过下标来滚到到估算的位置上，然后再判断有无，没有就一直往下滚到一个高度，直到找到）
4. 渲染区域高度一般需要的是固定值，如果页面发生变化或者页面窗口出现调节可以通过自定义的方法和resize来重新计算高度并更新

### 请解释什么是 ARIA 和屏幕阅读器 (screenreaders)，以及如何使网站实现无障碍访问 (accessible)。
ARIA（Accessible Rich Internet Applications）‌是一种技术规范，旨在提高网页和Web应用程序的可访问性。ARIA是WAI-ARIA（Web Accessibility Initiative - Accessible Rich Internet Applications）的一部分，它通过为HTML元素提供额外的角色（role）、状态（state）和属性（property），帮助屏幕阅读器等辅助技术更好地理解网页内容，从而使得视觉障碍、听觉障碍、运动障碍等用户能够无障碍地使用网站‌12。

‌屏幕阅读器（Screen Readers）‌是一种辅助技术，用于帮助视觉障碍用户通过语音或盲文等方式获取信息。屏幕阅读器可以读取网页内容，并将其转换为语音输出，帮助用户理解网页上的信息。通过使用ARIA，屏幕阅读器能够更准确地识别和处理网页中的动态内容和交互元素，从而提供更好的用户体验‌23。

‌实现网站无障碍访问的方法‌：  

1. ‌使用ARIA角色（role）‌：为HTML元素指定正确的ARIA角色，帮助屏幕阅读器理解元素的用途。例如，使用`role="button"`来标识一个可点击的元素。      
‌2. 状态和属性‌：使用ARIA的状态和属性来描述元素的当前状态或提供额外的信息。例如，`aria-pressed="true"`表示一个按钮当前被按下。      
‌3. 标记关键内容‌：使用`aria-label`或`aria-labelledby`属性来为无法通过视觉直接识别的元素提供文本标签。     
‌4. 动态内容‌：对于动态变化的内容，使用`aria-live`属性来指示屏幕阅读器在内容更新时进行朗读。    
‌5. 表单控件‌：对于复杂的表单控件，使用`ARIA`属性来描述其状态和功能，确保屏幕阅读器能够正确识别和操作。        

通过以上方法，可以显著提升网站的可访问性，使得所有用户都能无障碍地使用网站  


### vue常见优化手段
1. 使用key
2. 使用冻结的对象
3. 使用函数式组件
4. 使用计算属性
5. 非实时绑定的表单项
6. 保持对象引用稳定
7. 使用v-show替代v-if
8. 使用延迟装载（defer）
9. 使用keep-alive
10. 长列表优化
11. 打包体积优化

### webpack 打包优化
[打包体积的分析和优化【渡一教育】](https://www.bilibili.com/video/BV19z4y1P7xp/?share_source=copy_web&vd_source=ac7b22a8a616c6ac6cfb5e6a9219e959)

首先使用`webpack Bundle Analyzer`可视化工具，可以帮助我们直观地看到各个模块的大小分布。

1. 如果你的大型项目使用了乾坤等微前端框架来分成多个子项目，并且这些子项目都引用了相同的依赖，那么通过CDN来引用这些依赖并配置正确的缓存策略是一个有效的性能优化方法。在同一域名下，浏览器会共享这些资源的缓存，从而加快加载速度并提高用户体验。
```html
   <% if(NODE_ENV === "production")	{ %>	
   <script src="https://cdn.bootcdn.net/ajax/libs/vue/2.6.12/vue.min.js"></script>
   <script src="https://cdn.bootcdn.net/ajax/libs/vuex/3.5.1/vuex.min.js"></script>
   <script src="https://cdn.bootcdn.net/ajax/libs/ vue-router/3.4.7/vue-router.min.js"></script>
   <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.21.0/axios .min.js"></script>
   <% } %>
```

2. 针对浏览器兼容性打包两个版本（core-js和Babel在新版浏览器可以酌情引用）     
打包为两个版本后使用nginx代理并检测浏览器版本，来判断进入哪个项目    
```js
server {
    listen 80;
    server_name your_domain.com;

    # 检测User-Agent并重写URL
    location / {
        # 这是一个简化的示例，实际中需要根据具体的User-Agent字符串进行匹配
        if ($http_user_agent ~* "MSIE [6-8]|Firefox/[1-3]\.|Safari/[1-5]\.|Opera/[7-9]\.|Trident") {
            # 如果是老版本浏览器，重写URL到兼容版本项目包
            rewrite ^/(.*)$ /old_project/$1 last;
        }
        # 否则，默认访问新版本项目包
        rewrite ^/(.*)$ /new_project/$1 last;
    }

    # 配置old_project的根目录和静态文件处理
    location /old_project/ {
        alias /path/to/old_project/;
        try_files $uri $uri/ /old_project/index.html;
    }

    # 配置new_project的根目录和静态文件处理
    location /new_project/ {
        alias /path/to/new_project/;
        try_files $uri $uri/ /new_project/index.html;
    }

    # 其他配置，如错误页面、日志等
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

    # ... 其他配置 ...
}
```

<details> 
   <summary>更多</summary> 


Webpack是一个现代化的前端构建工具，用于打包和构建项目中的各种资源文件。以下是一些Webpack的优化手段：

一、减少入口文件大小和优化加载速度     
1. 拆分入口文件：将入口文件拆分为多个较小的模块，使用动态导入（dynamic imports）按需加载，减少初始加载的文件大小。      
2. 代码分割：通过配置Webpack的代码分割功能，将项目代码分割成多个块（chunks），并在需要的时候按需加载。      
3. 使用插件：如MiniCssExtractPlugin来提取CSS代码，减少构建时间和加载时间。    
4. 利用缓存：使用babel-loader的缓存机制等，以减少构建时间。    

二、优化文件体积     
1. Tree Shaking：通过配置Webpack的Tree Shaking功能，只保留项目中实际使用到的代码，剔除未使用的代码，从而减少打包后的文件大小。      
2. 压缩代码：     
   + 使用Webpack的压缩插件如terser-webpack-plugin来压缩JavaScript代码。      
   + 使用cssnano等工具压缩CSS代码。      
   + 使用image-webpack-loader等工具压缩图片资源。 

三、提升构建速度     
1. 并行构建：使用Webpack的thread-loader或happypack插件将任务分发给多个子进程并行处理，提高构建速度。     
2. 利用缓存：配置Webpack的缓存功能，使得构建过程中只重新构建发生更改的部分，而不是每次都重新构建整个项目。     
3. 优化loader配置：     
   + 使用oneOf配置加载器，使其文件只能匹配其中的一个loader，避免不必要的遍历。     
   + 通过include和exclude属性，只包含或排除某些文件，减少处理文件的数量。    

四、优化用户体验     
1. 懒加载与预加载：     
   + 对于大型应用，使用Webpack的懒加载（Dynamic Import）功能，按需加载非关键性资源。     
   + 使用预加载（Preload）和预解析（Prefetch）机制提前加载关键资源。      
2. 优化图片资源：    
+ 使用Webpack的url-loader或file-loader来压缩和处理图片。      
+ 根据需要进行懒加载或响应式加载。    

五、其他优化手段     
1. Source Map：在开发模式下生成更准确的source-map，以便在代码出错时快速定位到源代码的位置。在生产模式下，可以生成更小的源映射，以平衡性能和准确性。      
2. 模块解析优化：通过配置Webpack的resolve选项，设置合适的模块解析规则，避免过多的文件查找和解析过程。    
3. Bundle Analyzer：使用webpack-bundle-analyzer来查看打包后的bundle文件的体积，然后进行相应的体积优化。     
4. Gzip压缩：使用compression-webpack-plugin插件对打包后的文件进行Gzip压缩，提高传输效率。 

综上所述，Webpack的优化手段多种多样，涵盖了减少入口文件大小、优化文件体积、提升构建速度、优化用户体验以及其他方面的优化。这些优化手段可以根据具体项目需求和场景灵活应用，以提升Webpack的构建性能和用户体验。      
   
</details> 



### web Worker

 作用：允许主线程创建 Worker 线程，将一些任务分配给后者运行。在主线程运行的同时，Worker 线程在后台运行，两者互不干扰。等到 Worker 线程完成计算任务，再把结果返回给主线程。这样的好处是，一些计算密集型或高延迟的任务，被 Worker 线程负担了，主线程（通常负责 UI 交互）就会很流畅，不会被阻塞或拖慢。

 注意点：

1. 线程安全：
   + Web Workers 运行在独立的线程中，这意味着它们有自己的全局作用域和内存空间。因此，它们不能直接访问主线程中的变量或 DOM。
   + 数据需要在主线程和 Worker 之间通过 postMessage 方法进行传递。由于数据是通过结构化克隆算法进行复制的，因此传递的是数据的副本，而不是引用。
2. 通信开销：
   + 尽管 Web Workers 提供了在主线程和 Worker 之间进行通信的能力，但这种通信是有开销的。频繁地发送和接收大量数据可能会导致性能问题。
   + 为了最小化通信开销，可以考虑将任务拆分成较小的块，并在必要时才进行通信。
3. 错误处理：
   + Worker 中的代码可能会抛出错误或遇到异常情况。由于 Worker 运行在独立的线程中，这些错误不会直接传播到主线程。
   + 需要在 Worker 中添加适当的错误处理逻辑，并通过 postMessage 方法将错误信息发送回主线程进行处理。
4. 资源限制：
   + 每个浏览器对 Web Workers 的数量和资源使用都有一定的限制。例如，可能限制了可以同时创建的 Worker 数量，或者限制了 Worker 可以使用的内存量。
   + 在开发过程中，需要注意这些限制，并确保应用程序在受限条件下仍然能够正常工作。
5. 兼容性：
   + 尽管现代浏览器普遍支持 Web Workers，但并非所有浏览器都支持所有版本的 Web Workers API。
   + 在使用 Web Workers 之前，应该检查目标浏览器的兼容性，并考虑提供适当的回退机制。
6. 调试和测试：
   + 由于 Worker 运行在独立的线程中，传统的调试工具可能无法直接应用于 Worker 代码。
   + 可以使用 console.log、console.error 等方法来输出调试信息，并通过主线程和 Worker 之间的通信来传递这些信息。
   + 还可以考虑使用专门的调试工具或库来简化 Worker 代码的调试过程。
7. 终止 Worker：
   + 当不再需要 Worker 时，应该通过调用 terminate 方法来终止它。这有助于释放系统资源并避免潜在的内存泄漏。
   + 需要注意的是，一旦 Worker 被终止，它将无法再接收消息或执行任何代码。
8. 数据同步：
   + 如果主线程和 Worker 之间需要共享数据并保持同步，那么需要实现一种数据同步机制。
   + 这可能涉及到使用共享内存（如 SharedArrayBuffer 和 Atomics API）或其他同步原语来确保数据的一致性和正确性。

使用场景：
   执行耗时任务、处理大量数据、处理复杂逻辑。


使用：

1. 创建一个名为 worker.js 的文件       
这个文件不能访问 DOM，但它可以执行计算任务、处理数据等。
```js
// worker.js
self.onmessage = function(event) {
    // 从主线程接收到的数据
    const data = event.data;
    
    // 执行一些计算任务，例如计算一个数组的和
    let sum = 0;
    for (let i = 0; i < data.length; i++) {
        sum += data;
    }
    
    // 将结果发送回主线程
    self.postMessage(sum);
};
```

2. 在主线程中创建 Worker 实例       
在你的主 JavaScript 文件中，你需要创建一个 Worker 实例，并指定 Worker 文件的路径。
```js
// main.js
if (window.Worker) {
    // 创建 Worker 实例
    const myWorker = new Worker('worker.js');
    
    // 向 Worker 发送数据
    const dataArray = [1, 2, 3, 4, 5];
    myWorker.postMessage(dataArray);
    
    // 监听来自 Worker 的消息
    myWorker.onmessage = function(event) {
        console.log('Result from worker:', event.data); // 输出 Worker 计算的结果
    };
    
    // 监听 Worker 错误
    myWorker.onerror = function(error) {
        console.error('Error from worker:', error.message);
    };
} else {
    console.log('Your browser does not support Web Workers.');
}
```

3. 运行你的代码   
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Web Worker Example</title>
</head>
<body>
    <h1>Web Worker Example</h1>
    <script src="main.js"></script>
</body>
</html>
```


### 如何修改第三方npm包

如果遇到第三方包有bug或者需求不一样的情况。需要更改第三方npm包。

1. patch-package 是一个非常实用的工具，专门用于修复第三方依赖包。 

<details> 
   <summary>如何使用patch-package</summary>

1. 安装  
`npm install patch-package --save-dev`

2. 修改依赖包     
假设你需要修改`some-package`中的某个文件，你可以直接在`node_modules`目录下进行修改。

3. 生成补丁文件            
修改完成后，运行以下命令生成补丁文件：    
`npx patch-package some-package`    
这会在你的项目根目录下生成一个 patches 文件夹，其中包含生成的补丁文件（记得提交到git）。    

4. 配置 postinstall 脚本      
为了确保每次安装依赖时都能自动应用补丁，你需要在 package.json 中添加 postinstall 脚本：      
```js
{
  "scripts": {
    "postinstall": "patch-package"
  }
}
```

注意：         
patch是锁定版本号的，如果升级了版本，patch内容将会失效，最好在package.json能够锁定版本号。      
patch能支持多少文件修改，没有仔细测过，或许只能支持少量修改    
</details>


2. 直接在第三方包中更改（但是需要每次都把修改后的包发给没有node_modules包的同事）。    
3. 向原作者提issue，或者Fork该仓库代码，修改以后，提交合并请求。（费时间）


### 页面渲染百万条数据的表格
1. 分页。
2. 虚拟化（只渲染可见区域内的数据行）。
3. 懒加载（结合IntersectionObserver实现，触底加载下一页）。
4. 优化DOM（使用v-if。避免使用复杂计算属性）。
5. 减少DOM层级。
6. 使用Web Workers
7. 使用canvas


### 描述一下TCP三次握手的过程。
### 介绍下Set、Map、WeakSet和WeakMap 的区别？？？
### 在浏览器的开发者工具中，你如何定位和修复一个JavaScript错误？ 
### 描述一下JavaScript中的“事件循环”是什么，以及它在异步编程中起到什么作用？
[实例](https://zhuanlan.zhihu.com/p/696494576)

### 你如何检测和优化网页的加载速度？
### 请解释一下什么是MVVM设计模式，以及它在前端框架如React和Vue中的作用。
### 你如何对一个大型的前端项目进行代码调试？

### Vue的双向数据绑定是如何实现的？ 描述在实际项目中，如何利用这一特性提升表单交互的效率。
### 请解释Vue中的响应式系统，并说明在项目中如何利用它进行数据绑定和更新视图。
### Vue组件的props和事件在实际开发中如何使用？请举一个具体的交互场景。
### Vue组件间通信有多种方式，请描述在不同场景下（如父子、兄弟、跨组件）你选择哪种通信方式，并给出理由
### 请描述Vue的计算属性和侦听器在实际项目中的应用场景，并解释两者之间的区别。
### Vue项目中如何使用Vue Router实现路由权限控制?Vue项目中如何进行错误监控和异常处理，提高应用稳定性?
### Vue中如何利用虚拟列表(如vue-virtual-scroller)优化长列表性能?
### Vue项目中如何实现服务端渲染(SSR)，并解释为何选择SSR.
### Vue项目中如何进行性能优化，包括但不限于组件缓存、懒加载等方面?

### 在Vue项目中，如何设计和实现一个状态管理模块，以应对复杂的数据流和组件间通信?

### 浏览器的无痕模式怎么实现的，怎么破解，又怎么防御。   
[浏览器无痕模式破解](https://www.browserscan.net/zh)    



### Vue2、Vue3与React
### Vue、React的SEO
### 自定义的SEO优化
### Nuxt.js用不了的生命周期？
### axios如何做node、浏览器？
### 大文件下载暂停
### 优化的指标
### 计算首屏时间

### Webpack
### 网络
### HTTP2对于HTTP1.1
### TCP和UDP的区别
### Web安全防御详解
### babel原理
### babel和polyfill
### 前端错误监控
### 自定义错误监控
### 前端项目规范
### husky原理

### 技术选型考虑？      
跨平台和扩展性。人气，生态，扩展，维护活跃度


### 组件库维护
与业务耦合性较高，调试困难，需要进入具体组件内部进行调试（软链接）
menorepo+pnpm模式，来控制组件库和项目中的
[monorepo](https://blog.itpub.net/70027824/viewspace-3007404/)

### 不同水平的开发者如何做到统一和效率提示
+ 文档
+ 整体架构图
+ 开发规范，代码校验
+ 封装组件，可配置组件。

### 前端优化做过哪些？
+ lodash使用才打包，用 lodash-es


### vite和webpack区别？


### vue3和vue2对比




### map 和对象的区别
+ map key是有序的

### 最有挑战性的功能

+  离线功能，有网和无网的扭转。

### 判断对象是否有环引用
+ 深度变量。（判断是一个对象，就放到数组中，如果下次还是一个对象，就去看是否有相同的对象，对比）

### nextTick原理？微任务还是宏任务


### Promise链式调用


### 老项目精度丢失。小数相加
+ 打包时用webpack插件


### 文件太大，cdn
+ 使用外链的方法来加载


### 你如何实现类公告，10条数据，无限循环滚动，无缝滚动的？
### Promise为什么可以链式调用
### nextTick为什么可以获取dom更新后的数据
### 你最常用的git命令是什么，如果要删除远程分支命令是什么
### websocket长链接，如何保持的。如果断开又怎么处理
### js的堆和栈

### 使用 pnpm 快速配置 monorepo
