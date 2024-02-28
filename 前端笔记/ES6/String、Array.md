## String
### 属性

属性 | 描述
---|---
constructor | 对创建该对象的函数的引用
length | 字符串的长度
prototype | 允许您向对象添加属性和方法

### 方法
方法 | 描述
---|--- 
charAt() | 返回在指定位置的字符。
charCodeAt() | 返回在指定的位置的字符的 Unicode 编码。
==concat()==<br>concat(stringX,stringX,...,stringX)| 连接字符串。
==indexOf()==<br>indexOf(searchvalue,fromindex?) | 检索字符串。
==lastIndexOf()==<br>lastIndexOf(searchvalue,fromindex?) | 从后向前搜索字符串。
match() | 找到一个或多个正则表达式的匹配。
replace() | 替换与正则表达式匹配的子串。
==slice(start,end)== | 	提取字符串的片断，并在新的字符串中返回被提取的部分。
==split()== | 把字符串分割为字符串数组。
==substr(start,length?)== | 从起始索引号提取字符串中指定数目的字符。
==substring(start,stop?)== | 	提取字符串中两个指定的索引号之间的字符。
toLowerCase() | 把字符串转换为小写。
toUpperCase() | 把字符串转换为大写。
trim() | 去除字符串两边的空白
toString() | 返回字符串。
valueOf() | 返回某个字符串对象的原始值。


#### reverse

## Array
### 方法


方法 | 描述
---|---
==concat()== | 连接两个或更多的数组，并返回结果。
copyWithin() | 从数组的指定位置拷贝元素到数组的另一个指定位置中。
entries() | 返回数组的可迭代对象。
every() | 检测数值元素的每个元素是否都符合条件。
fill() | 使用一个固定值来填充数组。
==filter()== | 检测数值元素，并返回符合条件所有元素的数组。
==find()== | 返回符合传入测试（函数）条件的数组元素。
==findIndex()== | 返回符合传入测试（函数）条件的数组元素索引。
==forEach()== | 数组每个元素都执行一次回调函数。
from() | 通过给定的对象中创建一个数组。
==includes()== | 判断一个数组是否包含一个指定的值。
indexOf() | 搜索数组中的元素，并返回它所在的位置。
isArray() | 判断对象是否为数组。
==join()== | 把数组的所有元素放入一个字符串。
keys() | 返回数组的可迭代对象，包含原始数组的键(key)。
lastIndexOf() | 搜索数组中的元素，并返回它最后出现的位置。
==map()== | 通过指定函数处理数组的每个元素，并返回处理后的数组。
pop() | 删除数组的最后一个元素并返回删除的元素。
push() | 向数组的末尾添加一个或更多元素，并返回新的长度。
reduce() | 将数组元素计算为一个值（从左到右）。
reduceRight() | 将数组元素计算为一个值（从右到左）。
reverse() | 反转数组的元素顺序。
shift() | 删除并返回数组的第一个元素。
==slice()== | 选取数组的的一部分，并返回一个新数组。
some() | 检测数组元素中是否有元素符合指定条件。
sort() | 对数组的元素进行排序。
==splice()== | 从数组中添加或删除元素。
toString() | 把数组转换为字符串，并返回结果。
unshift() | 向数组的开头添加一个或更多元素，并返回新的长度。
valueOf() | 返回数组对象的原始值。


#### 1.0 定义和实例方法（...）
Array是一种特殊的对象，所以typeof([1,2,3]) => "object"
#### 1.1 拓展运算符（...）
...[] 将一个数组转为用逗号分隔的参数序列。
```
console.log(...[1,2,3]) => 1 2 3
console.log(1,...[2,3,4],5) => 1 2 3 4 5
```
替代函数的 apply 方法

```
Math.max.apply(null, [14, 3, 77])
=> Math.max(...[14, 3, 77])
=> Math.max(14, 3, 77);
```
[1,2,3]后面添加[4,5]

```
let arr1 = [1, 2, 3];
let arr2 = [4, 5];
arr1.push(...arr2);
```
#### 1.2 扩展运算符(...)的应用
克隆数组（修改a2不改变a1）

```
const a1 = [1, 2];
// a2只是复制了a1的指针，并不是克隆的全新数组
const a2 = a1;
a2[0] = 2;
a1 // [2, 2]    修改a2使a1改变

// ES5运用concat克隆了a1到a2
const a2 = a1.concat();
a2[0] = 2;
a1 // [1, 2]    修改a2但a1未改变

// ES6用(...)克隆的简便写法
const a2 = [...a1];
const [...a2] = a1;
```
合并数组

```
// 注意以下都是浅拷贝，修改arr123会影响arr4
const arr1 = ['a', 'b'];
const arr2 = ['c'];
const arr3 = ['d', 'e'];
// ES5 的合并数组
const arr4 = arr1.concat(arr2, arr3);
// ES6 的合并数组
const arr4 = [...arr1, ...arr2, ...arr3]
```
与解构赋值结合

```
// 注意扩展运算符只能放在最后，否则报错
const [first, ...rest] = [1, 2, 3, 4, 5];
first // 1
rest  // [2, 3, 4, 5]

const [first, ...rest] = [];
first // undefined
rest  // []

const [first, ...rest] = ["foo"];
first  // "foo"
rest   // []
```
处理字符串'hello'=>['h','e','l','l','o',]

```
[...'hello'] => ['h','e','l','l','o']
'hello'.split('') => ['h','e','l','l','o']
```
Map 和 Set 结构，Generator 函数结合

```
let map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);
let arr = [...map.keys()]; // [1, 2, 3]

const go = function*(){
  yield 1;
  yield 2;
  yield 3;
};
[...go()] // [1, 2, 3]
```
如果对没有 Iterator 接口的对象，使用扩展运算符，将会报错

```
const obj = {a: 1, b: 2};
let arr = [...obj]; // TypeError: Cannot spread non-iterable object
```
#### 2.1 Array.from()

类似数组的对象（本质特征只有一点，即必须有length属性。）<br>
Array.from将它转为真正的数组。
```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};

// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']
// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```
只要是部署了 Iterator 接口的数据结构<br>
Array.from都能将其转为数组。
```js
Array.from('hello')
// ['h', 'e', 'l', 'l', 'o']

let namesSet = new Set(['a', 'b'])
Array.from(namesSet) // ['a', 'b']

Array.from([1, 2, 3])
// [1, 2, 3]
```
扩展运算符（...）也可以将某些数据结构转为数组。