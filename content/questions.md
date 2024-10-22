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

### 描述一下TCP三次握手的过程。
### 在浏览器的开发者工具中，你如何定位和修复一个JavaScript错误？ 
### 解释一下CSS中的“级联”规则是什么，以及它是如何工作的？
### 你如何解决CSS的穿透性问题？
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
### 请谈谈你喜欢的开发环境。
### 你最熟悉哪一套版本控制系统?
### 你能描述当你制作一个网页的工作流程吗?
### 假若你有 5 个不同的样式文件 (stylesheets), 整合进网站的最好方式是?
### 你能描述渐进增强 (progressive enhancement) 和优雅降级 (graceful degradation) 之间的不同吗?
### 你如何对网站的文件和资源进行优化?
### 浏览器同一时间可以从一个域名下载多少资源?
### 请说出三种减少页面加载时间的方法。(加载时间指感知的时间或者实际加载时间)
### 如果你参与到一个项目中，发现他们使用 Tab 来缩进代码，但是你喜欢空格，你会怎么做?
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


### js的垃圾回收基础，有什么问题，如何优化
### js的堆和栈
