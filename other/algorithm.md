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
