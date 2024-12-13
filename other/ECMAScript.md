ECMAScript所有版本

> ECMAScript 262（ECMA-262）是JavaScript语言的一个标准化规范，由Ecma国际（前身为欧洲计算机制造商协会）制定。ECMAScript采用年号来做版本命名。   
> https://ecma-international.org/publications-and-standards/standards/ecma-262/


## ECMAScript 1 - 1997

+ JavaScript 的首次标准化，基于 Netscape JavaScript 1.1 和 Microsoft JScript。
+ 定义了核心语言特性：
  + 基本数据类型：`undefined、Null、Boolean、Number、String、Object`。
  + 运算符：
    + 算术运算符：`+, -, *, /, %`
    + 比较运算符：`<, >, <=, >=, ==, !=`
    + 逻辑运算符：`&&, ||, !`
    + 赋值运算符：`=, +=, -=, *=, /=`
    + 字符串连接运算符：`+` 用于字符串拼接。

  + 控制语句：`if、for、switch、while` 等。
  + 基本内置对象：`Global、Math、Date`（最初较简化）。

## ECMAScript 2 - 1998

+ 修订第 1 版的规范错误。
+ 针对国际化需求做了部分调整，但没有添加新的语言特性。

## ECMAScript 3  - 1999

+ 引入了大量关键特性，是现代 JavaScript 的基础：
  + 正则表达式：添加了全面支持。
  + 异常处理：引入 try...catch。
  + 新语句：do...while、switch、continue、break。
  + 字符串和数组增强：新增多种方法（如 Array.prototype.sort、String.prototype.replace）。
  + 更完善的全局对象。



## ECMAScript 4  - 2008 （被取消）

+ 这是一个未完成的版本，开发工作在 2003 年至 2008 年间进行，后因复杂性和意见分歧而取消。
+ 原计划引入许多新特性，包括：
  + 类、模块和类型注解。
  + 更先进的继承模型。
  + 静态类型检查。
  + 部分特性在后续的 ECMAScript 5 和 6 中逐步实现。


## ECMAScript 5  - 2009

+ 这是一个现代 JavaScript 的重要版本：
  + 严格模式：通过 "use strict"; 提高代码安全性和规范性。
  + 属性描述符：引入 Object.defineProperty。
  + JSON 支持：原生支持 JSON.parse 和 JSON.stringify。
  + 数组方法：如 map、filter、forEach、reduce。
  + 其他小改进：bind 方法、Object.keys 等。

## ECMAScript 5.1 - 2011

+ 几乎没有新增功能，主要是与 ISO/IEC 16262 保持一致。
  + 对一些不明确的地方进行了补充说明
  + 提升了对多语言和国际化场景的兼容性。
  + 通过 ISO/IEC 的审核，使 ECMAScript 成为全球公认的标准，方便在更多场景中应用。

## ECMAScript 6  - 2015

+ JavaScript 史上最重要的更新之一，现代 JS 的核心：
  + 块级作用域：let 和 const。
  + 类与继承：class 和 extends。
  + 箭头函数：简化函数表达式，支持词法作用域。
  + 模板字符串：使用反引号 ${} 插值。
  + 默认参数和剩余参数。
  + 模块化：import 和 export。
  + Promise：异步操作的标准化支持。
  + 其他：Symbol 类型、Map/Set 数据结构、for...of、生成器函数。

## ECMAScript 7  - 2016
+ 两个主要特性：
  + 指数运算符：**。
  + Array.prototype.includes：检查数组是否包含某个值。


## ECMAScript 8  - 2017

  + 异步函数：async/await。
  + 共享内存：SharedArrayBuffer 和 Atomics。
  + Object.values 和 Object.entries：对象迭代的增强。
  + 字符串填充方法：padStart 和 padEnd。

## ECMAScript 9  - 2018

  + 异步迭代器：for await...of。
  + 正则表达式增强：
  + 命名捕获组。
  + 后行断言。
  + dotAll 模式（s 修饰符）。
  + Rest/Spread 支持对象。

## ECMAScript 10  - 2019

  + Array.prototype.flat 和 flatMap：数组扁平化方法。
  + Object.fromEntries：对象生成方法。
  + 可选 catch 绑定：try...catch 中的 catch 可以省略参数。
  + 字符串 trimStart 和 trimEnd。
  + JSON 超集：支持 U+2028 和 U+2029。

## ECMAScript 11  - 2020

  + 可选链运算符：?.。
  + 空值合并运算符：??。
  + 动态 import()。
  + 全局对象 globalThis。
  + BigInt：支持大整数计算。
  + Promise.allSettled：处理多个 Promise 的所有结果。

## ECMAScript 12  - 2021

  + 逻辑赋值运算符：&&=, ||=, ??=。
  + Promise.any：只等待第一个成功的 Promise。
  + 字符串 replaceAll 方法。
  + WeakRefs 和 FinalizationRegistry：内存管理增强。

## ECMAScript 13  - 2022

  + 类字段和私有方法：正式支持。
  + 顶层 await：模块级别支持 await。
  + Error.cause：为错误对象添加原因说明。
  + 正则表达式 d 标志：支持索引捕获。

## ECMAScript 14  - 2023

  + Array 和 TypedArray 方法：toSorted, toReversed, toSpliced, with。
  + Symbol.prototype.description：改进符号描述。
  + 装饰器：正式引入类的装饰器支持。