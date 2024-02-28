## Promise
### 1. Promise的含义
Promise 是一个对象，代表一个异步操作，
Promise对象有以下两个特点。
1. 对象的状态不受外界影响。有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。
2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise对象的状态改变，只有两种可能：从pending变为fulfilled和从pending变为rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。

### 2. 基本用法
Promise对象是一个构造函数，用来生成Promise实例。
```js
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```
Promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数。
```js
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```
Promise 新建后就会立即执行。then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行。  
p2的resolve方法将p1作为参数，即一个异步操作的结果是返回另一个异步操作。
```js
const p1 = new Promise(function (resolve, reject) {
  console.info('p1');
  setTimeout(() => reject(new Error('fail')), 3000)
})
const p2 = new Promise(function (resolve, reject) {
  console.info('p2');
  setTimeout(() => resolve(p1), 1000)
})
p2
  .then(result => console.log(result))
  .catch(error => console.log(error))
console.info('cccccccc');

// 'p1'
// 'p2'
// 'cccccccc'
// [Error: fail]
```

p1的状态决定了p2的状态。如果p1的状态是pending，那么p2的回调函数就会等待p1的状态改变；如果p1的状态已经是resolved或者rejected，那么p2的回调函数将会立刻执行。

### 3 .then()

then方法的第一个参数是resolved状态的回调函数，第二个参数（可选）是rejected状态的回调函数。  
then方法返回的是一个新的Promise实例（注意，不是原来那个Promise实例）。因此可以采用链式写法，即then方法后面再调用另一个then方法。
```js
getJSON("/post/1.json").then(
  post => getJSON(post.commentURL)
).then(
  comments => console.log("resolved: ", comments),
  err => console.log("rejected: ", err)
);
```

### 4 .catch()
相当于.then(null, rejection)或.then(undefined, rejection)的别名，用于指定发生错误时的回调函数。
```js
const promise = new Promise(function(resolve, reject) {
  reject(new Error('a'));
  throw new Error('b');
});
promise.catch(function(error) {
  console.log(error);
});
// Error: a
```
如果 Promise 状态已经变成resolved，再抛出错误是无效的。  
因为 Promise 的状态一旦改变，就永久保持该状态，不会再变了。

**一般then不要定义reject，用catch()去获取错误。**  
Promise 对象的错误具有“冒泡”性质，会一直向后传递，直到被捕获为止。也就是说，错误总是会被下一个catch语句捕获。  
```js
getJSON('/post/1.json').then(function(post) {
  return getJSON(post.commentURL);
}).then(function(comments) {
  // some code
}).catch(function(error) {
  // 处理前面三个Promise产生的错误
});
```
上面代码中，一共有三个 Promise 对象：一个由getJSON()产生，两个由then()产生。它们之中任何一个抛出的错误，都会被最后一个catch()捕获。

如果没有使用catch()方法指定错误处理的回调函数，Promise 对象抛出的错误不会传递到外层代码，即不会有任何反应。
