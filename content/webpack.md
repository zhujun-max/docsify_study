
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

