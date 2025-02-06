### 数组操作函数

| 对象                     | 作用                                               | 返回值                   | 改变原数组 |
| ------------------------ | -------------------------------------------------- | ------------------------ | ---------- |
| push()                   | 向数组的末尾添加一个或多个元素                     | 返回新数组的长度         | 是         |
| pop()                    | 删除数组的最后一个元素                             | 返回删除的值             | 是         |
| unshift()                | 数组的头部添加一个或多个元素                       | 返回新数组的长度     | 是         |
| shift()                  | 删除数组的第一个元素                               | 返回删除的值             | 是         |
| reverse()                | 颠倒数组中的元素顺序                               | 返回颠倒后的值           | 是         |
| sort(a,b)                | 对数组元素进行排序（会先调用toString方法，然后按照字符串序列排序。也可以自定义排序）sort((a, b) => b - a) | 返回排序后的值  | 是 |
| splice(start, end,value) | 可以删除，插入，替换 | 返回被替换/删除/插入的值 | 是 |
| isArray()					|用于检测是否为数组|返回true，false|否|
| toString()		|把元素转换为字符串，默认以逗号分割		|返回字符串|否|
| forEach(item,index,arr) | 对所有元素执行函数，常用来遍历元素 | 无 | 否 |
| every(item,index,arr)	|对所有元素执行函数，全部都为true，返回true	|返回true，false|否|
| some()	|对所有元素执行函数，有一个为true，返回true	|返回true，false|否|
| filter(item,index,arr)	|对所有元素执行函数(自定义函数)	|返回满足条件的值|否|
| map(item,index,arr)	|对所有元素执行函数	|返回自定义函数结果|否|
| concat()                 | 拼接两个或多个数组                               | 返回合并的值             | 否         |
| join()                   | 把元素转成字符串，使用指定符号分割                 | 返回分割后的字符串        | 否         |
| slice(start, end)        | 截取元素                                           | 返回截取的值             | 否         |
| toString()  | 将数组用逗号隔开        | 返回字符串  | 否         |
| slice(start, end)  | 复制指定位置元素        | 返回数组中被选中的元素  | 否         |
| indexOf(x, start)        | 查找元素第一次出现的位置。只能使用数组中的值         | 返回下标，没找到返回-1   | 否         |
| lastIndexOf(x,start)  | 查找元素最后一次出现的位置。只能使用数组中的值          | 返回下标，没找到返回-1   | 否         |
| findIndex()  | 查找元素第一次出现的位置。可以使用回调函数         | 返回下标，没找到返回-1   | 否         |
| find()  | 查找元素第一次出现的位置。可以使用回调函数         | 返回元素值，没找到返回undefined   | 否         |
| includes(x,start)  | 查找元素是否包含指定的值        | 返回true和false  | 否         |


**数组**
+ at(index): 返回数组中指定位置的元素，允许使用负数索引来从数组末尾开始计数。
+ concat(...items): 合并两个或多个数组，并返回一个新数组，原数组不会被修改。
+ constructor: 返回创建数组实例的 Array 构造函数。
+ copyWithin(target, start[, end]): 在当前数组内部，将指定位置的成员复制到另一个指定位置，并返回这个数组。不会修改原数组的长度，也不会创建新数组。
+ entries(): 返回一个新的数组迭代器对象，该对象包含数组中每个索引的键/值对。
+ every(callback[, thisArg]): 测试数组的所有元素是否都通过了指定函数的测试。如果所有元素都通过测试，则返回 true；否则返回 false。
+ fill(value[, start[, end]]): 用一个静态值填充一个数组从起始索引到终止索引内的所有元素，并返回这个数组。
+ filter(callback[, thisArg]): 创建一个新数组，其包含通过所提供函数实现的测试的所有元素。
+ find(callback[, thisArg]): 返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined。
+ findIndex(callback[, thisArg]): 返回数组中满足提供的测试函数的第一个元素的索引。否则返回 -1。
+ flat([depth]): 将一个多维数组拉平成一个一维数组。depth 参数指定要拉平的嵌套层数，默认为 1。
+ flatMap(callback[, thisArg]): 首先使用映射函数映射每个元素，然后将结果展平成一个新数组。
+ forEach(callback[, thisArg]): 为数组中的每个元素执行一次提供的函数。
+ includes(valueToFind[, fromIndex]): 判断一个数组是否包含一个指定的值，根据情况指定搜索的起始位置。
+ indexOf(searchElement[, fromIndex]): 返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回 -1。
+ join(separator): 将数组的所有元素连接成一个字符串。
+ keys(): 返回一个新的数组迭代器对象，该对象包含数组中的每个索引键。
+ lastIndexOf(searchElement[, fromIndex]): 返回在数组中可以找到一个给定元素的最后一个索引，如果不存在，则返回 -1。
+ length: 返回数组的长度。
+ map(callback[, thisArg]): 创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。
+ pop(): 移除数组的最后一个元素，并返回该元素。
+ push(...elements): 将一个或多个元素添加到数组的末尾，并返回新的长度。
+ reduce(callback[, initialValue]): 对数组中的每个元素执行一个提供的函数（升序执行），将其结果汇总为单个返回值。
+ reduceRight(callback[, initialValue]): 对数组中的每个元素执行一个提供的函数（降序执行），将其结果汇总为单个返回值。
+ reverse(): 反转数组的元素顺序，并返回该数组。
+ shift(): 移除数组的第一个元素，并返回该元素。
+ slice([begin[, end]]): 返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝。原数组不会被修改。
+ some(callback[, thisArg]): 测试数组中的某些元素是否通过了指定函数的测试。如果通过了测试，则返回 true；否则返回 false。
+ sort([compareFunction]): 对数组的元素进行排序并返回数组。排序可以是数字或字符串。
+ splice(start[, deleteCount[, item1[, item2[, ...]]]]): 通过删除或替换现有元素或者添加新元素来修改数组，并返回被删除的元素。
+ toLocaleString(): 返回一个字符串，该字符串表示数组中的所有元素，且根据本地时间惯例进行格式化。
+ toString(): 返回表示数组及其元素的字符串。
+ unshift(...elements): 将一个或多个元素添加到数组的开头，并返回新的长度。
+ values(): 返回一个新的数组迭代器对象，该对象包含数组中的每个值。

**String**
+ anchor(name): 创建一个 HTML 锚 (`<a>`) 元素，其 name 属性设置为指定的文本。
+ at(index): 返回在指定位置的字符。允许使用负数索引从字符串末尾开始计数。
+ charAt(index): 返回指定位置的字符。
+ charCodeAt(index): 返回在指定位置的字符的 Unicode 编码。
+ codePointAt(index): 返回给定索引处的 UTF-16 编码单元的值，如果那是一个代理对（即高代理项和低代理项组成的一个 Unicode 字符），则返回该字符的完整 Unicode 码点。
+ concat(string2, string3, ..., stringN): 连接一个或多个字符串，并返回新的字符串。
+ constructor: 返回创建字符串对象的构造函数。
+ endsWith(searchString[, length]): 判断字符串是否以指定的子字符串结尾，根据可选的 length 参数限制搜索的字符数。
+ includes(searchString[, position]): 判断一个字符串是否包含在另一个字符串中，根据情况指定搜索的起始位置。
+ indexOf(searchValue[, fromIndex]): 返回在字符串中首次找到指定值的索引，如果没有找到则返回 -1。可以指定搜索的起始位置。
+ isWellFormed(): 检查一个字符串是否是规范形式的 UTF-16 序列（此方法在 ECMAScript 标准中未定义，可能特定于某些环境）。
+ lastIndexOf(searchValue[, fromIndex]): 返回在字符串中最后一次找到指定值的索引，如果没有找到则返回 -1。可以指定搜索的起始位置。
+ length: 返回字符串的长度。
+ localeCompare(that[, locales[, options]]): 使用本地特定的顺序比较两个字符串，并返回指示字符串排序顺序的数字。
+ match(regexp): 检索返回一个字符串匹配正则表达式的结果。返回一个数组，其中存放匹配的结果。如果没有找到匹配项，则返回 null。
+ matchAll(regexp): 返回一个包含所有匹配正则表达式及分组捕获结果的迭代器。
+ normalize([form]): 返回调用字符串值的指定 Unicode 正规形式。
+ padEnd(targetLength[, padString]): 在当前字符串的末尾填充指定的字符串，直到达到目标长度。填充的字符串默认为空格。
+ padStart(targetLength[, padString]): 在当前字符串的开头填充指定的字符串，直到达到目标长度。填充的字符串默认为空格。
+ repeat(count): 返回一个新字符串，该字符串包含调用该方法的字符串的指定数量的副本。
+ replace(searchValue, newValue): 在字符串中查找一个匹配项，然后替换与正则表达式或子字符串匹配的结果。
+ replaceAll(searchValue, newValue): 返回一个新字符串，所有匹配 searchValue 的地方都被 newValue 替换（与 replace 类似，但替换所有匹配项）。
+ search(regexp): 执行正则表达式和字符串之间的搜索匹配。返回匹配项的索引。
+ slice(beginIndex[, endIndex]): 提取字符串的片段，并在新的字符串中返回被提取的部分。
+ split(separator[, limit]): 通过将字符串分割成子字符串数组，来将一个字符串分割成字符串数组。
+ startsWith(searchString[, position]): 判断字符串是否以指定的子字符串开头，根据可选的 position 参数限制搜索的起始位置。
+ substr(start[, length]): 从起始索引号提取字符串中指定数量的字符。
+ substring(start[, end]): 提取字符串中介于两个指定下标之间的字符。
+ toLocaleLowerCase(): 根据任何指定区域设置的规则把字符串转换为小写。
+ toLocaleUpperCase(): 根据任何指定区域设置的规则把字符串转换为大写。
+ toLowerCase(): 将字符串转换为小写。
+ toString(): 返回字符串的字符串表示。
+ toUpperCase(): 将字符串转换为大写。
+ toWellFormed(): 检查一个字符串是否是规范形式的 UTF-16 序列，并返回一个新的字符串（此方法在 ECMAScript 标准中未定义，可能特定于某些环境）。
+ trim(): 去除字符串两端的空白字符。
+ trimEnd(): 去除字符串末尾的空白字符。
+ trimLeft(): 同 trimStart()，去除字符串开头的空白字符。
+ trimRight(): 同 trimEnd()，去除字符串末尾的空白字符。
+ trimStart(): 去除字符串开头的空白字符。
+ valueOf(): 返回指定对象的原始值。对于字符串对象，直接返回字符串本身。
+ ~~big(): 已废弃。使用 CSS 来代替，使字符串以大字体显示。~~
+ ~~blink(): 已废弃。使用 CSS 动画来代替，使字符串闪烁。~~
+ ~~bold(): 已废弃。使用 CSS 来代替，使字符串以粗体显示。~~
+ ~~fixed(): 已废弃。使用 CSS 来代替，以打字机字体显示字符串。~~
+ ~~fontcolor(color): 已废弃。使用 CSS 来代替，设置字符串的颜色。~~
+ ~~fontsize(size): 已废弃。使用 CSS 来代替，设置字符串的字体大小。~~
+ ~~italics(): 已废弃。使用 CSS 来代替，使字符串以斜体显示。~~
+ ~~link(url): 已废弃。创建一个 HTML 链接 (`<a>`) 元素，其 href 属性设置为指定的 URL。~~
+ ~~small(): 已废弃。使用 CSS 来代替，使字符串以小字体显示。~~
+ ~~strike(): 已废弃。使用 CSS 来代替，在字符串上添加删除线。~~
+ ~~sub(): 已废弃。使用 CSS 来代替，将字符串设置为下标。~~
+ ~~sup(): 已废弃。使用 CSS 来代替，将字符串设置为上标。~~  

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


## 二维数组扩展只取需要的内容

```js
a.map((v) => {
  return b.children.map((vv) => {
    return {
      swid: vv.name,
      mrid: vv.mrId,
      dwName: vv.name,
    };
  });
}).flat();
```

## 循环查找相同的内容，改变找到的内容

```js
a.map((v) => {
  b.some((vv) => {
    if (v.name === vv.name) {
      vv["id"] = v.id;
      return true;
    }
  });
});
```

## 数组对比，查找差异

```js
Array.prototype.minus = function (arr) {
  var result = new Array();
  var obj = {};
  for (var i = 0; i < arr.length; i++) {
    obj[arr[i]] = 1;
  }
  for (var j = 0; j < this.length; j++) {
    if (!obj[this[j]]) {
      obj[this[j]] = 1;
      result.push(this[j]);
    }
  }
  return result;
};
// 获取数组a多出的部分
console.log(a.minus(b));
// 获取数组b多出的部分
console.log(b.minus(a));
```

## 数组中的数组，匹配内容，返回参数

```js
const flattened = data.flatMap((item) => item.children);

// 使用find方法查找匹配的mrid对应的对象
const foundObject = flattened.find((obj) => obj.mrid === mridToFind);

// 如果找到了匹配的对象，返回它的swid，否则返回null
return foundObject ? foundObject.swid : null;
```
