## 1. 模板区（template）

1. canvas 的宽高只能通过在行内设置 width 和 height，不能使用 css 设置，否则会导致图形拉伸
2. 当低版本的浏览器不支持 canvas 标记时，会把 canvas 展示为一个普通的标记，就会显示在 canvas 内部写的提示语，而如果浏览器支持 canvas,内部的提示语则不会显示

```
<canvas width="700" height="700" ref="canvas">
        您的浏览器版本过低,不支持canvas,请升级浏览器或使用chrome浏览器
</canvas>
```

## 2. 样式区（style 区）

canvas 实际上是一个内联元素，要设置它在页面水平居中，需要把它设置为块级元素
<br>（再次声明，不可以在 css 里设置 canvas 的宽高）

```
canvas {
    display: block;
    margin: 0 auto;
    border: solid 2px #999;
}
```

## 3. 脚本区(script 区)

canvas 应该在 mounted 的生命周期中初始化，在 created 和 updated 中都是无效的。

```
export default {
  mounted() {
    this.initCancas()
  },
}
```

```
<script setup>
onMounted(() => {
	initCancas();
}
const initCancas = () => {
}
</script>
```

### canvas 坐标

canvas 是一个二维网格，左上角坐标为（0，0），x 轴向右为正，y 轴向下为正，上面的 fillRect 方法拥有参数（10，10，100，80）意思是：在画布上绘制 100x80 的矩形，从坐标（10，10）开始。

### 3.1 获得 canvas

两个的区别就是：

1. 用 ref 找到的 canvas 使用时需要使用 canvas.value,<br>
2. 而 document.querySelector 找到的 canvas 使用时不需要加.value

```html
<script setup>
	import { onMounted, ref } from "vue"; // 从vue导入钩子函数和ref

	// 找到canvas节点，可以使用js的document寻找，也可以使用vue的ref寻找

	const canvas = document.querySelector("canvas");

	const canvas = ref(null);
</script>
```

### 3.2 获取画笔

```js
const ctx = canvas.getContext("2d"); // 使用document找到的

const ctx = canvas.value.getContext("2d"); // 使用ref找到的
```

### 3.3 画线（两点确定一条直线）

```js
ctx.beginPath(); // 开启一条路径
ctx.moveTo(x1, y1); // 将画笔移动到一个点
ctx.lineTo(x2, y2); // 将画笔移动到第二个点
ctx.strokeStyle = "#333"; // 设置描边的颜色
ctx.width = 3; // 设置线宽，取值为数值
ctx.stroke(); // 开始画
ctx.closePath(); // 关闭路径
```

### 3.4 画矩形

```js
ctx.beginPath(); // 如果不重新开启路径，会和上一次画的连上
ctx.fillStyle = "#0f0"; // 填充样式
ctx.fillRect(x1, y1, x2, y2); // 填充
ctx.closePath();
```

### 3.5 擦除

```
ctx.clearRect(x1, y1, x2, y2)
```

### 3.6 画圆

```
ctx.beginPath() // 开启新路径
ctx.arc(x1, y1, 圆形半径, 角度值1, 角度值2,顺时针还是逆时针)
// 例如
ctx.arc(100, 100, 100, 0, Math.PI, true);
ctx.stroke()
```

### 3.7 画字（写字）

```
ctx.font = '30px 微软雅黑'

ctx.fillText('文字内容', x1, y1)

ctx.fillText('canvas',100, 100) // 实心文字

ctx.strokeText('canvas', 100, 100) // 空心文字
```

### 3.8 canvas 转换 base64 地址

```
//用ref找到的元素，要加.value
let base64 = canvas.value.toDataURL('image/jpeg', 1);
```

### 3.9 下载 canvas 画的图

```
// 模板区绑定的save方法
cosnt save = () => {
    canvas.value.toBlob(blob => {
        let blobURL = URL.createObjectURL(blob);
        let aNode = document.createElement('a')
        aNode.href = blobURL
        aNode.download = 'Canvas图片'
        aNode.click()
    })
}
```

### 3.10 加载图片并加文字水印

```
let img = new Image()
image.src = '要加载的图片路径'
image.onload = () => {
    ctx.beginPath()
    ctx.drawImage(img, x1, y1)
    ctx.font = '30px 宋体'
    ctx.fillText('这是水印', x1, y1)
}
```

## 响应式画布

当需要使用 canvas 铺满全屏时，直接使用 css 声明达不到理想的效果。

```
//错误的效果，会造成图像变形拉伸
canvas{
    width: 100px;
    height: 100px
}
```

正确的做法是给 canvas 的宽高赋值：

```
let canvas = document.getElementById('myCanvas');
let ctx = canvas.getContext('2d');
let winW = window.innerWidth
let winH = window.innerHeight
canvas.width = winW
canvas.height = winH
```

### 响应式画布：

```
let canvas;
let ctx;
export default {
  mounted() {
    this.initCancas()    // 当调整窗口大小时重绘canvas
    window.onresize = () => {
      this.initCanvas()
    }
  },
  methods: {
    initCanvas() {
      console.log("初始化canvas")
      canvas = document.getElementById('myCanvas');
      ctx = canvas.getContext('2d');
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
      this.drawCanvas()
    },
    drawCanvas() {
      ctx.beginPath();
      ctx.moveTo(20, 20);
      ctx.lineTo(140, 70);
      ctx.lineWidth = 1.0;
      ctx.strokeStyle = '#cc0000'
      ctx.stroke()
    }
  }
}
```
