## Set
Set是不包含重复值的数组（自动去重）

Set 结构没有键名，只有键值（或者说键名和键值是同一个值）
### Set的基本用法
```js
const s = new Set();
[1,2,3,4,4,4,5].forEach(o => s.add(o))
s // => {1,2,3,4,5}

const set = new Set([1,2,3,3,3]);
set // => {1,2,3}
[...set] // => [1,2,3]
set.size // => 5
```
#### 1.1 Set给数组和字符串去重
```js
// 数组
[...new Set(Array)]
// 字符串
[...new Set('aabbccdd')].join('') // => 'abcd'
```
向 Set 加入值的时候，不会发生类型转换，所以5和"5"是两个不同的值。
a = {}, b = {}，也是不同的值。
但a = NaN, b = NaN，是同一个值
```js
var set = new Set();
set.add(5); // => {5}
set.add('5'); // => {5, '5'}
set.add(NaN); // => {5, '5', NaN}
set.add(NaN) // => {5, '5', NaN}
set.add({}) // => {5, '5', NaN, {} }
set.add({}) // => {5, '5', NaN, {}, {} }
```
#### 1.2 Set的属性和方法
属性：
- constructor => 构造函数，默认就是Set函数。
- size => 返回Set实例的成员总数。

方法
- add() => 返回Set本身
- delete() => 返回boolean，true为删除成功
- has() => 返回boolean，判断是否为Set成员
- clear() => 不返回值

#### 1.3 判断Set有没有某键字段和Obj判断不同
```js
const obj = {aaa: 'vvv'}
obj['aaa'] // => 'vvv'

const set = new Set(['aaa', 'bbb'])
set['aaa'] // => undefined
set.has('aaa') // => true
```
#### 1.4 使用Array.from把Set转Array数组
```js
const set = new Set([1,2,3,4,4,4]);
const arr = Array.from(set);    // => [1,2,3,4]
```
### 遍历操作
- Set.prototype.keys() => 返回键名的遍历器
- Set.prototype.values() => 返回键值的遍历器
- Set.prototype.entries() => 返回键值对的遍历器
- Set.prototype.forEach() => 使用回调函数遍历每个成员

#### 2.1 keys()、values()、entries()
```js
const set = new Set([1,2,3]);

for (let item of set.keys()) {
    // 1 2 3
}
for (let item of set.values()) {
    // 1 2 3
}
for (let item of set.entries()) {
    // [1,1] [2,2] [3,3]
}
```
Set 结构的实例默认可遍历，它的默认遍历器生成函数就是它的values方法。
```js
Set.prototype[Symbol.iterator] === Set.prototype.values
```
所以可以省略values()，直接循环遍历Set
```js
for (let item of set) {}
```
#### 2.2 forEach()
```js
set.forEach((value, key) => {
    console.info(value);    // 键值
    console.info(key);  // 键名
})
```

#### 2.3 遍历的应用
数组的map和filter方法也可以间接用于 Set 
```js
let set = new Set([1, 2, 3]);
set = new Set([...set].map(x => x * 3));
set // => {3, 6, 9}
// 获得{3,6,9}的另一种方法
set = new Set(Array.from(set, val => val * 3));
set // => {3, 6, 9}

set = new Set([...set].filter(x => (x % 2) == 0));
set // => {6}
```
用Set方便实现并集、交集、差集
```js
let a = new Set([1,2,3]);
let b = new Set([2,3,4]);

// 并集
let union = new Set([...a, ...b]);

// 交集
let intersect = new Set([...a].filter(o => b.has(o)));

// 差集
let difference = new Set([...a].filter(o => !b.has(o)));
```

## Map
Object：本质上是键值对的集合（Hash 结构），只能用字符串当作键

Map：各种类型的值（包括对象）都可以当作键
### Map的基本用法
```js
const map = new Map();
const o = {aaa: 'bbb'};

map.set(o, 'ccc');  // => {{'aaa': 'bbb'} => 'ccc'}
map.get(o); // => 'ccc'

map.has(o); // true
map.delete(o);  // true
map.has(o); //false
```
#### 1.1 使用数组构造Map
```js
const map = new Map([
    ['aaa', '111'], ['bbb', '222']
]);

map // => {'aaa' => '111', 'bbb' => '222'}
map.size    // => 2
map.has('aaa') // true
map.get('aaa') // '111'
```
#### 1.2 使用Set和Map，构造新的Map
任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构（详见《Iterator》一章）都可以当作Map构造函数的参数。

所以Set和Map都能当做键值对数据结构对象，构造新的Map
```js
// 用Set构造Map
const set = new Set([
    ['aaa', '111'], ['bbb', '222']
]);
set // => {['aaa', '111'], ['bbb', '222']}

const map1 = new Map(set);
map1 // => {"aaa" => "111", "bbb" => "222"}
map1.get('aaa') // => '111'

// 用Map构造新的Map
const map2 = new Map(['ccc', '333']);
map2 // => {'ccc' => '333'}
const map3 = new Map(map2);
map3 // => {'ccc' => '333'}
map3.get('ccc') // '333'
```

#### 1.3 Map对同一键可以覆盖赋值
对键1连续赋值两次，后一次的值覆盖前一次的值。
```js
const map = new Map();
map.set(1,'111').set(1,'222').set(3, '333');
map // {1 => '222', 3 => '333'}
```
如果 Map 的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map 将其视为一个键

undefined和null也是两个不同的键。

虽然NaN不严格相等于自身，但 Map 将其视为同一个键。
```js
let map = new Map();

map.set(-0, 123);
map.get(+0) // 123

map.set(undefined, 3);
map.set(null, 4);
map.get(undefined) // 3

map.set(NaN, 123);
map.get(NaN) // 123
```

#### （注意：只有对同一个对象的引用，Map 结构才将其视为同一个键）
```js
const map = new Map();
const k1 = ['a'];
const k2 = ['a'];

map.set(['a'], 555);
map
.set(k1, 111)
.set(k2, 222);

map.get(['a']) // undefined
map.get(k1) // 111
map.get(k2) // 222
```
这就解决了同名属性碰撞（clash）的问题，我们扩展别人的库的时候，如果使用对象作为键名，就不用担心自己的属性与原作者的属性同名。

### Map实例的属性和方法

属性：
- constructor => 构造函数，默认就是Map函数。
- size => 返回Map实例的成员总数。

方法
- set (key, value) => 返回Map本身
- get (key) => 返回键值value
- has (key) => 返回boolean，判断是否为Set成员
- delete (key) => 返回boolean，true为删除成功
- clear() => 不返回值

### 遍历方法
- Map.prototype.keys() => 返回键名的遍历器
- Map.prototype.values() => 返回键值的遍历器
- Map.prototype.entries() => 返回键值对的遍历器
- Map.prototype.forEach() => 使用回调函数遍历每个成员

```js
const map = new Map([['aaa', '111'], ['bbb', '222']]);
map // { 'aaa' => '111', 'bbb' => '222' }

for (let item of map.keys()) {
    // 'aaa' 'bbb'
}
for (let item of map.values()) {
    // '111' '222'
}
for (let item of map.entries()) {
    // ['aaa', '111']  ['bbb', '222']
}
// Map 结构的默认遍历器接口（Symbol.iterator属性），就是entries方法
map[Symbol.iterator] === map.entries;    // true
for (let [key, value] of map) {
  // ['aaa', '111']  ['bbb', '222']
}
```
#### 2.1 Map转List
```js
const map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

[...map.keys()]
// [1, 2, 3]

[...map.values()]
// ['one', 'two', 'three']

[...map.entries()]
// [[1,'one'], [2, 'two'], [3, 'three']]

[...map]
// [[1,'one'], [2, 'two'], [3, 'three']]
```

 
