## 空格

```
&nbsp; ：不换行空格，一个字符的半角的不断行的空格，如果需要在网页中插入多个空格，可以将“&nbsp;”代码写多遍；
&ensp; ：“半角空格”，一个字符的半角的空格，也可以将“&ensp;”写多遍来插入多个空格；
&emsp; ：两个字符的全角的空格，也可以将“&emsp;”写多遍来插入更多的空格；
&thinsp; ：小于一个字符的空格；
```


## div阻止点击穿透+实现点击穿透
一、阻止点击穿透，上层点击时加上下面这句，阻止事件冒泡到父元素
```
event.stopPropagation();
```

二、点击穿透到下面一层，不点击上层，为上层添加下面样式代码即可

```
pointer-events: none;
```
示例代码

```html
<!DOCTYPE html>
<html>
<head>
  <title>阻止点击穿透/实现点击穿透</title>
  <style>
    div{
      float: left;
    }
    .under{
      width: 300px;
      height: 150px;
      padding: 20px;
      margin: 20px;
      background: #5b7e91;
    }
    .up{
      width: 50px;
      height: 50px;
      line-height: 50px;
      border-radius: 10px;
      background: #ec6800;
      text-align: center;
      color: #fff;
    }
    .noclick{
      pointer-events: none;  /* 上层加上这句样式可以实现点击穿透 */
    }
  </style>
</head>
<body>

  <div class="under" onclick="under()">
    <p>阻止点击穿透</p>
    <div class="up" onclick="up()">点我</div>
  </div>

  <div class="under" onclick="under()">
    <p>点击穿透</p>
    <div class="up noclick" onclick="up()">点我</div>
  </div>
  <script>
    var under = function() {
      alert("点击下层")
    }
    var up = function() {
      event.stopPropagation();    // 上层加上这行代码，可以阻止点击穿透
      alert("点击上层")
    }
  </script>
</body>
</html>
```
https://blog.csdn.net/weixin_36270908/article/details/100575779

## 滚动条样式
![image](https://www.w3cways.com/wp-content/uploads/2014/09/scrollbarparts.png)

#### webkit下面的CSS设置滚动条
1. ::-webkit-scrollbar 滚动条整体部分，可以设置宽度啥的
1. ::-webkit-scrollbar-button 滚动条两端的按钮
1. ::-webkit-scrollbar-track  外层轨道
1. ::-webkit-scrollbar-track-piece  内层滚动槽
1. ::-webkit-scrollbar-thumb 滚动的滑块
1. ::-webkit-scrollbar-corner 边角
1. ::-webkit-resizer 定义右下角拖动块的样式

#### IE下面的CSS设置滚动条
1. scrollbar-arrow-color: color; /*三角箭头的颜色*/
1. scrollbar-face-color: color; /*立体滚动条的颜色（包括箭头部分的背景色）*/
1. scrollbar-3dlight-color: color; /*立体滚动条亮边的颜色*/
1. scrollbar-highlight-color: color; /*滚动条的高亮颜色（左阴影？）*/
1. scrollbar-shadow-color: color; /*立体滚动条阴影的颜色*/
1. scrollbar-darkshadow-color: color; /*立体滚动条外阴影的颜色*/
1. scrollbar-track-color: color; /*立体滚动条背景颜色*/
1. scrollbar-base-color:color; /*滚动条的基色*/


## 超过长度省略号
```
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```
- white-space: nowrap; 保证文本内容不会自动换行，如果多余的内容会在水平方向撑破单元格。
- overflow: hidden 隐藏超出单元格的部分。
- text-overflow: ellipsis 将被隐藏的那部分用省略号代替。


## 横向文字按钮自动靠右
```html
<div class="custom-tree-node" v-for="(item, index) in linkwbsList" :key="index">
	<span class="info-label">{{ item.objectFullName }}</span>
	<span>
		<el-button type="text" @click="event => zoomto(item)">
			切换到wbs
		</el-button>
		<el-divider direction="vertical"></el-divider>
		<el-button type="text" @click="event => zoomto(item)">
			定位
		</el-button>
	</span>
</div>
```
```css
::v-deep .custom-tree-node {
	flex: 1;
	display: flex;
	align-items: center;
	justify-content: space-between;
	font-size: 14px;
	padding-right: 8px;
	.info-label {
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		max-width: 240px;
	}
}
```


## table只让tbody滚动
```html
  <table>
    <thead>
      <tr>
        <th>记录名称</th>
        <th>行政区域</th>
        <th>记录人</th>
        <th>状态</th>
        <th>已交地</th>
        <th>拟使用时间</th>
      </tr>
    </thead>
    <tbody>
      <tr *ngFor="let item of dataLists">
        <td>
          <label nz-checkbox [(ngModel)]="checked">2019-10-02 马边县征地进度记录</label>
        </td>
        <td>马边县</td>
        <td>记录员A</td>
        <td>已交地</td>
        <td>2786</td>
        <td>2019-10-03</td>
      </tr>
    </tbody>
  </table>
```

```css
table tbody {
    display:block;
    height:195px;
    overflow-y:scroll;
}
table thead, tbody tr {
    display:table;
    width:100%;
    table-layout:fixed;
}
table thead {
    width: calc( 100% - 1em )
}
```

## width:100vh以及calc(100vh + 10px)
#### vh/vw
vh: 相对于视窗的高度, 视窗被均分为100单位的vh;<br>
vw: 相对于视窗的宽度, 视窗被均分为100单位的vw;

vmax: 相对于视窗的宽度或高度中较大的那个。其中最大的那个被均分为100单位的vmax;<br>
vmin: 相对于视窗的宽度或高度中较小的那个。其中最小的那个被均分为100单位的vmin;

**视区**<br>
所指为浏览器内部的可视区域大小，<br>
即window.innerWidth/window.innerHeight大小，不包含任务栏标题栏以及底部工具栏的浏览器区域大小。

#### calc
calc是英文单词calculate(计算)的缩写，是css3的一个新增的功能，用来指定元素的长度。比如说，你可以使用calc()给元素的border、margin、pading、font-size和width等属性设置动态值。为何说是动态值呢?因为我们使用的表达式来得到的值。不过calc()最大的好处就是用在流体布局上，可以通过calc()计算得到元素的宽度。

- 用于动态计算长度值。
- 需要注意的是，运算符前后都需要保留一个空格，例如：width: calc(100% - 10px)；
- 任何长度值都可以使用calc()函数进行计算；
- calc()函数支持 “+”, “-“, “*”, “/” 运算；
- calc()函数使用标准的数学运算优先级规则；


```
calc(100vh - 10px)  表示整个浏览器窗口高度减去10px的大小
calc(100vw - 10px)   表示整个浏览器窗口宽度减去10px的大小
```

## http请求  特殊字符+消失了

- 最多使用的应为encodeURIComponent，它是将中文、韩文等特殊字符转换成utf-8格式的url编码，
- 所以如果给后台传递参数需要使用encodeURIComponent时需要后台解码对utf-8支持（form中的编码方式和当前页面编码方式相同） 
- escape不编码字符有69个：*，+，-，.，/，@，_，0-9，a-z，A-Z 
- encodeURI不编码字符有82个：!，#，$，&，'，(，)，*，+，,，-，.，/，:，;，=，?，@，_，~，0-9，a-z，A-Z 
- encodeURIComponent不编码字符有71个：!， '，(，)，*，-，.，_，~，0-9，a-z，A-Z 

javascript中可用的编码解码函数，有如下的组合： 

```
escape(string); 
unescape(string);
encodeURI(string); 
decodeURI(string);
encodeURIComponent(string); 
decodeURIComponent(string);
```

## 滚动到指定位置
```
const item = document.getElementById('monthDiv');
if (item) {
  item.scrollIntoView({
    behavior: 'smooth',
    block: 'start',
    inline: 'start',
  });
}
```

## 监控页面按键
```
ngOnInit() {
    // 增加回车监控事件
    window.addEventListener('keydown', this.keyDown);
}
ngDestroy() {
    window.removeEventListener('keydown', this.keyDown, false);
}

// 回车登陆
keyDown = (e) => {
    if (e.keyCode === 13) {
      this.submit();
    }
};
```
## 判断是否移动端
```
// 判断是否是移动端
export const isMobile = () => {
  var sUserAgent = navigator.userAgent.toLowerCase();
  var bIsIpad = sUserAgent.match(/ipad/i);
  var bIsIphoneOs = sUserAgent.match(/iphone os/i);
  var bIsMidp = sUserAgent.match(/midp/i);
  var bIsUc7 = sUserAgent.match(/rv:1.2.3.4/i);
  var bIsUc = sUserAgent.match(/ucweb/i);
  var bIsAndroid = sUserAgent.match(/android/i);
  var bIsCE = sUserAgent.match(/windows ce/i);
  var bIsWM = sUserAgent.match(/windows mobile/i);
  if (bIsIpad || bIsIphoneOs || bIsMidp || bIsUc7 || bIsUc || bIsAndroid || bIsCE || bIsWM) {
    //设备为移动端
    return true;
  } else {
    return false;
  }
};
```

## 页面指向其它网址
```
window.location.href = 'https://www.baidu.com/';
```

## js下载文件到本地各种方法总结\
> 当不加download属性时，如果文件格式为txt、pdf、jpg等浏览器支持直接打开的文件格式，那么不会下载，而是浏览器直接打开；添加download属性之后，就会下载，并且下载文件默认命名为你download属性的值。
```
<a href="../../static/xxx.xlsx" download="xxx.xlsx">下载</a>
window.open('./assets/年度投资计划导入模板.xlsx');
window.open("https://mp.csdn.net/postedit/static/xxx.xlsx")
```
更多

https://www.cnblogs.com/xiong950413/p/14209813.html