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

### 运行大量个耗时并且会占用主线程的任务，保证页面不卡顿
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
   比如一个域名下有两个子项目，两个子项目中都要存储`userInfo`。为了防止数据互相污染，就**给对应的项目加上前缀**。

+ **注意版本，迭代防范**   
   项目更新之前`userInfo`用来存的字符串，更新后存的对象，存取方式不一样，容易报错。每次更改内容，可以**添加一个版本号**

+ **时效性**    
   存数据时，加入一个时间戳，取数据时做判断

+  **兼容 SSR（服务端渲染）**   
   在服务端是使用不了 localStorage 的，因为不是浏览器环境，所以你像封装一个比较通用的 localStorage，得兼顾 SSR 的情况

+ **加密**

+ **存入取出类型转换（注意考虑map、set、Date类型）**  
   使用`instanceof`判断类型，存入的时候添加类型，取出的时候根据类型判断就行。

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

### 你能描述渐进增强 (progressive enhancement) 和优雅降级 (graceful degradation) 之间的不同吗?
**渐进增强：**针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。（从被所有浏览器支持的基本功能开始，逐步地添加那些只有新式浏览器才支持的功能，向页面添加无害于基础浏览器的额外样式和功能。当浏览器支持时，它们会自动地呈现出来并发挥作用。）

**优雅降级：**一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。（Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会检查以确认它们是否能正常工作。由于IE独特的盒模型布局问题，针对不同版本的IE的hack实践过优雅降级了，为那些无法支持功能的浏览器增加候选方案，使之在旧式浏览器上以某种形式降级体验却不至于完全失效。）

**区别：**优雅降级是从复杂的现状开始，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的、能够起作用的版本开始，并不断扩充，以适应未来环境的需要。

### 假若你有 5 个不同的样式文件 (stylesheets), 整合进网站的最好方式是?

根据class命名规则写样式，这样样式不会冲突，提取公共的样式，进行合并，非公共的单独拎出来。然后打包压缩一下就行了，若每个文件都很大，就需要分模块加载。

### 你能描述当你制作一个网页的工作流程吗?

内容分析：分清展现在网络中内容的层次和逻辑关系

结构设计：写出合理的html结构代码

布局设计：使用html+css进行布局

样式设计：首先要使用reset.css

交互设计：鼠标特效

行为设计：js代码，ajax页面行为和从服务器获取数据

测试兼容性；优化性能。

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

### 描述一下TCP三次握手的过程。
### 在浏览器的开发者工具中，你如何定位和修复一个JavaScript错误？ 
### 描述一下JavaScript中的“事件循环”是什么，以及它在异步编程中起到什么作用？
### 你如何实现一个简单的Promise？
### 你如何检测和优化网页的加载速度？
### 请解释一下“Ajax”是什么，以及它在改善网站性能中的作用。
### 为什么说“避免使用内联事件处理器”是好的实践？
### 请解释一下什么是MVVM设计模式，以及它在前端框架如React和Vue中的作用。
### 什么是单元测试？为什么在前端开发中它们是重要的？
### 请解释一下持续集成/持续部署（CI/CD）是什么，以及为什么它们在现代Web开发中如此重要。
### 你如何对一个大型的前端项目进行代码调试？
### 在制作一个网页应用或网站的过程中，你是如何考虑其 UI、安全性、高性能、SEO、可维护性以及技术因素的?


### 你如何对网站的文件和资源进行优化?
### 浏览器同一时间可以从一个域名下载多少资源?
### 请谈谈你对网页标准和标准制定机构重要性的理解。

### 请解释什么是 ARIA 和屏幕阅读器 (screenreaders)，以及如何使网站实现无障碍访问 (accessible)。

### 什么使 CORS，以及其要解决的问题?
### Koa2框架
### 介绍下深度优先遍历和广度优先遍历，如何实现?
### 介绍下Set、Map、WeakSet和WeakMap 的区别?
### sass 和 less的区别， 以及用过的方法
### Vue的双向数据绑定是如何实现的？ 描述在实际项目中，如何利用这一特性提升表单交互的效率。
### 请解释Vue中的响应式系统，并说明在项目中如何利用它进行数据绑定和更新视图。
### Vue组件的props和事件在实际开发中如何使用？请举一个具体的交互场景。
### Vue组件间通信有多种方式，请描述在不同场景下（如父子、兄弟、跨组件）你选择哪种通信方式，并给出理由
### 请描述Vue的计算属性和侦听器在实际项目中的应用场景，并解释两者之间的区别。
### Vue的指令(如v-if, v-for)在哪些具体场景下你会选择使用，为什么?
### Vue的生命周期钩子在项目开发中扮演什么角色?请举例说明至少三个常用钩子的使用场景。
### Vue的v-model指令在表单处理中如何使用?请结合一个实际表单验证的案例。
### Vue项目中如何使用Vue Router实现路由权限控制?Vue项目中如何进行错误监控和异常处理，提高应用稳定性?
### Vue中如何利用虚拟列表(如vue-virtual-scroller)优化长列表性能?
### Vue项目中如何实现服务端渲染(SSR)，并解释为何选择SSR.
### Vue项目中如何进行性能优化，包括但不限于组件缓存、懒加载等方面?
### Vue项目中如何实现单元测试和端到端测试，使用哪些测试工具?
### 在Vue项目中，如何设计和实现一个状态管理模块，以应对复杂的数据流和组件间通信?
### Vue的动态组件如何在SPA中实现页面的按需加载?
### 在一个实时消息系统中，如何使用Node.js实现消息的实时推送？
### 当处理大量并发的HTTP请求时，你如何优化Node.js应用的性能？
### 描述一种场景，在该场景中你将使用Node.js的中间件来处理请求。
### 如何使用Node.js和Express框架实现用户登录和权限管理系统？
### 在一个电商网站上，你如何使用Node.js处理支付功能？
### 描述一种场景，你将在Node.js应用中实现WebSocket通信。
### 假设你正在开发一个基于Node.js的博客系统，如何设计一个高效的数据存储方案？
### 在一个视频流应用中，如何使用Node.js进行视频流的实时处理？
### 当你的Node.js应用需要处理国际化和本地化时，你会如何设计它？
### 如何使用Node.js和Redis实现一个缓存系统？
### 描述一种场景，你需要在Node.js应用中实现负载均衡。
### 当你的Node.js应用需要处理大量的图片时，你如何优化图片处理流程？
### 如何使用Node.js进行性能测试和分析？
### 当你的Node.js应用需要处理大量的并发WebSocket连接时，你如何确保系统的稳定性？
### 如何使用Node.js和第三方库实现一个实时数据分析系统？
### 假设你正在开发一个基于Node.js的实时游戏服务器，你将如何设计服务器架构来支持大量玩家同时在线？
### 浏览器的无痕模式怎么实现的，怎么破解，又怎么防御。   
[浏览器无痕模式破解](https://www.browserscan.net/zh)    



> 第一天的面试题

### Vue2、Vue3与React
### Vue、React的SEO
### 自定义的SEO优化
### Nuxt.js用不了的生命周期？
### axios如何做node、浏览器？
### 大文件下载暂停
### 优化的指标
### 计算首屏时间
### webWorker
### 前端工程化
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
### 换肤
### 微前端
### 部署
### 单元测试


> 第二天的面试题

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
+ 

### Promise链式调用


### 老项目精度丢失。小数相加
+ 打包时用webpack插件

### 虚拟列表缺点时什么？
+ 预加载
+ 分页

### 文件太大，cdn
+ 使用外链的方法来加载

### git rebase和merage的区别

### git reset 和reverse


git    
https://leping.blog.csdn.net/article/details/136549736?spm=1001.2014.3001.5502   


### 如何知道自己项目适用于多少版本的node.js

第三天面试题

### 你如何实现类公告，10条数据，无限循环滚动，无缝滚动的？
### Promise为什么可以链式调用
### nextTick为什么可以获取dom更新后的数据
### 你最常用的git命令是什么，如果要删除远程分支命令是什么
### websocket长链接，如何保持的。如果断开又怎么处理



### js的堆和栈
