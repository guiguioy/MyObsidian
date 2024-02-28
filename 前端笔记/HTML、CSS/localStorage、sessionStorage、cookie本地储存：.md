[2022 年，前端本地存储有哪些主流方案？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/505031430)
# Localstorage的跨域存储方案

<https://www.jianshu.com/p/e86d92aeae69>
https://juejin.cn/post/6982759183179317279
## 1. **sessionStorage**

- sessionStorage 仅在当前会话下有效，关闭页面或浏览器后被清除；
- setItem(key,value) 设置数据
- getItem(key) 获取数据
- removeItem(key) 移除数据
- clear() 清除所有值

```jsx
<script>
    // 添加数据
   window.sessionStorage.setItem("name","李四")
   window.sessionStorage.setItem("age",18)
    // 获取数据
    console.log(window.sessionStorage.getItem("name")) // 李四
    // 清除某个数据
    window.sessionStorage.removeItem("gender")
    // 清空所有数据
    window.sessionStorage.clear()
</script>
```

## 2. **localStorage**

- localStorage 是 HTML5 标准中新加入的技术，用于长久保存整个网站的数据，保存的数据没有过期时间，直到手动去删除；
- localStorage 和 sessionStorage 最大一般为 5MB，仅在客户端（即浏览器）中保存，不参与和服务器的通信；
- setItem(key,value) 设置数据
- getItem(key) 获取数据
- removeItem(key) 移除数据
- clear() 清除所有值

```jsx
<script>
    // 添加数据
    window.localStorage.setItem("name","张三")
    window.localStorage.setItem("age",20)
    window.localStorage.setItem("gender","男")
    // 获取数据
    console.log(window.localStorage.getItem("name")) // 张三
    // 清除某个数据
    window.localStorage.removeItem("gender")
    // 清空所有数据
    window.localStorage.clear()
</script>
```

## 3. cookie

Cookie 是一些数据, 存储于你电脑上的文本文件中，用于存储 web 页面的用户信息

Cookie 数据是以键值对的形式存在的，每个键值对都有过期时间。如果不设置时间，浏览器关闭，cookie 就会消失，当然用户也可以手动清除 cookie

Cookie 每次都会携带在 HTTP 头中，如果使用 cookie 保存过多数据会带来性能问题

Cookie 内存大小受限，一般每个域名下是 4K 左右，每个域名大概能存储 50 个键值对

### 基本操作

通过访问 document.cookie 可以对 cookie 进行创建，修改与获取。

默认情况下，cookie 在浏览器关闭时删除，你还可以为 cookie 的某个键值对 添加一个过期时间

如果设置新的 cookie 时，某个 key 已经存在，则会更新这个 key 对应的值，否则他们会同时存在 cookie 中

```jsx
<script>
    // 设置cookie
    document.cookie = "username=orochiz"
    document.cookie = "age=20"
 
    // 读取cookie
    var msg = document.cookie
    console.log(msg) // username=orochiz; age=20
 
    // 添加过期时间（单位：天）
    var d = new Date() // 当前时间 2019-9-25
    var days = 3       // 3天
    d.setDate(d.getDate() + days)
    document.cookie = "username=orochiz;"+"expires="+d
 
    // 删除cookie （给某个键值对设置过期的时间）
    d.setDate(d.getDate() - 1)
    console.log(document.cookie)
</script>
```

# 总结

## **相同点：**

都保存在浏览器端，可以下图位置查看储存的信息

![image](https://img-blog.csdnimg.cn/20201011104234271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxOTI5NTc4,size_16,color_FFFFFF,t_70#pic_center)

## **不同点：**

### 1. **传递方式不同**

cookie 数据始终在同源的 http 请求中携带（即使不需要），即 cookie 在浏览器和服务器间来回传递。

sessionStorage和 localStorage 不会自动把数据发给服务器，仅在本地保存。

### 2. **数据大小不同**

cookie 数据还有路径（path）的概念，可以限制 cookie 只属于某个路径下。存储大小限制也不同，cookie 数据不能超过 4k，同时因为每次 http 请求都会携带 cookie，所以 cookie 只适合保存很小的数据，如会话标识。

sessionStorage 和localStorage虽然也有存储大小的限制，但比 cookie 大得多，可以达到 5M 或更大。

### 3. **数据有效期不同**

sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持；

localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；

cookie 只在设置的 cookie 过期时间之前一直有效，即使窗口或浏览器关闭。

### 4. **作用域不同**

sessionStorage 不在不同的浏览器窗口中共享，即使是同一个页面；

localStorage 在所有同源窗口中都是共享的；

cookie 也是在所有同源窗口中都是共享的。

Web Storage 支持事件通知机制，可以将数据更新的通知发送给监听者。

Web Storage 的 api 接口使用更方便。