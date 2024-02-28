
[link](https://blog.csdn.net/lyf1997115/article/details/82317411)
[link](http://www.divcss5.com/html/h53936.shtml)

## HTML常用标签详解
### 常见的块级标签
**常见的块级标签**

```
标题标签<h1></h1>...<h6></h6>
水平线<hr/>
段落<p></p>
换行<br/>
引用<blockquote</blockquote>
预格式<pre></pre>

引用标签<blockquote></blockquote>
表明标签中的文字，为引用的内容，浏览器显示为等宽字体，并缩进。
cite属性，表明引用的来源，一般为引用的网址URL
<blockquote cite="http：//www.yt4561761.com">
hahahahahahah
</blockquote>

预格式标签<pre></pre>
浏览器解析时，会按照等宽字体显示，并保留标签内的空格和回车。
常用于保留代码格式。
<pre>yt4561761
yt4561761
yt4561761
</pre>
```
**有序列表ol order list**

```
<ol>
    <li>一</li>
    <li>二</li>
    <li>三</li>
    <li>四</li>
</ol>
```
**无序列表ul unorder list**

```
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
</ul>
```
**定义描述列表**

一般情况下，标题dt只有一项。描述项dd可以有多项。
浏览器显示时，标题顶格显示，dd缩进显示。
```
<dl>
    <dt>这是dl列表的标题</dt>
    <dd>描述项1</dd>
    <dd>描述项2</dd>
    <dd>描述项3</dd>
</dl>
```
**图片组合标签figure**

```
1-<figure></figure>标签有两个子标签：
<img src="">:一幅图片，src表示图片的路径。
<figcaption></figcaption>：图片的标题
2-浏览器显示为：图片与标题上下排列，且整体向后缩进一个单位。

<figure>
    <img src="img/icon.png" />
    <figcaption>洪浩光伏
    </figcaption>
</figure>
```
**分区标签div**

```
常配合CSS使用，为网页中最常用的分区标签，常用于网页布局使用
<div style="width：100%; height：100px; ">
这是div里面的文字
<h1>div里面的标题</h1>
</div>
```

### 常见的行级标签
**常见的行级标签**

```
span 文本
img 图片
em 强调
strong 强调
q 短引用
a 超链接
i 倾斜
b 加粗
small 缩小字体
u 下划线

span（文本）：用于包裹一部分文字，进行特定样式的修改。
虞涛真<span style="color:red; font-size:36px;">酷</span>！！

em（强调）：浏览器显示为倾斜。
strong（强调）：浏览器显示为加粗。
```

**strong/em/i/b 标签的区别**

```
1-em和strong都表示强调，strong>em,strong和em标签均可多层嵌套，表示强调程度的递增。
2-em和i都能倾斜，Strong和b都能加粗。但是Strong和em多了一层强调的语义。可以帮助搜索 引擎快速抓取网站重点。且html5要求开发者尽可能实现代码的语义化。
<em>我真踏马帅！！</em><br />
<strong>我真籍八帅！！</strong><br />
<i>我被i标签弄斜了</i><br />
<b>我被b标签弄粗了</b><br />
```

**q(短引用)**
常用于一句话的引用，cite属性表示引用来源，浏览器解析时，会在内容的前后插入双引号。

```
<q cite="www.yt4561761.com">那你很棒哦</q>

small（缩小字体）：small标签可多层嵌套，表示比默认字体小一号，直到小到最小号为止。

big（放大字体）：亦可多层嵌套，直到最大。
但在最新规范中，small和big标签不提倡使用。提倡使用style="font-size:11px;"CSS样式替代。
<p>那你很<big><big><big><big><big>棒</big></big></big></big></big>哦！</p>
```
**img 图片标签**

```
1-src属性：表示图片引用路径。
常见路径的写法：
①相对路径：
Ⅰ -当图片在当前文件下一层时：文件夹名/图片名 例如：img/abc.jpg
Ⅱ-当图片与当前文件在同一层时：图片名 例如：src="abc.jpg"
Ⅲ-当图片在当前文件上一层时：../图片名 例如：src="../abc.jpg"
使用相对路径时，图片最外层只能放到网站根目录（图片必须要在项目文件夹中）
②绝对路径：写法file：///E:/aaa.png 但是，严禁使用
③网络连接：直接使用图片的网络地址，但由于图片在别的服务器，不可控，故不建议使用
2-title:图片的标题。当鼠标指上时，显示的提示文字。
3-alt：当图片无法加载时显示的文字。
4-width/height:图片的尺寸，相当于CSS中的style="width:"
5-align:图片周围的文字，相对于图片的排列方式。可选值：top/center/bottm
<img src="../img/285-1606240Z040347.jpg" title="漩涡鸣人"/>
<img src="[Liuyun&VCB-S]HanaSaku Iroha[01][Hi10p_1080p][BDRip][x264_flac_2ac3]_2015125173925.bmp"
title="松前绪花" alt="图片无法显示，请刷新"/>
<img src="pic/a947a8ec8a1363272535dd01938fa0ec09fac744.png" title="DEVIL MAY CRY"/>
```
### 表格标签
### 表单标签


**常见的语义化标签**

```
<title>：页面主体内容。
<hn>：h1~h6，分级标题，<h1> 与 <title> 协调有利于搜索引擎优化。
<ul>：无序列表。
<li>：有序列表。
<header>：页眉通常包括网站标志、主导航、全站链接以及搜索框。
<nav>：标记导航，仅对文档中重要的链接群使用。
<main>：页面主要内容，一个页面只能使用一次。如果是web应用，则包围其主要功能。
<article>：定义外部的内容，其中的内容独立于文档的其余部分。
<section>：定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。
<aside>：定义其所处内容之外的内容。如侧栏、文章的一组链接、广告、友情链接、相关产品列表等。
<footer>：页脚，只有当父级是body时，才是整个页面的页脚。
<small>：呈现小号字体效果，指定细则，输入免责声明、注解、署名、版权。
<strong>：和 em 标签一样，用于强调文本，但它强调的程度更强一些。
<em>：将其中的文本表示为强调的内容，表现为斜体。
<mark>：使用黄色突出显示部分文本。
<figure>：规定独立的流内容（图像、图表、照片、代码等等）（默认有40px左右margin）。
<figcaption>：定义 figure 元素的标题，应该被置于 figure 元素的第一个或最后一个子元素的位置。
<cite>：表示所包含的文本对某个参考文献的引用，比如书籍或者杂志的标题。
<blockquoto>：定义块引用，块引用拥有它们自己的空间。
<q>：短的引述（跨浏览器问题，尽量避免使用）。
<time>：datetime属性遵循特定格式，如果忽略此属性，文本内容必须是合法的日期或者时间格式。
<abbr>：简称或缩写。
<dfn>：定义术语元素，与定义必须紧挨着，可以在描述列表dl元素中使用。
<address>：作者、相关人士或组织的联系信息（电子邮件地址、指向联系信息页的链接）。
<del>：移除的内容。
<ins>：添加的内容。
<code>：标记代码。
<meter>：定义已知范围或分数值内的标量测量。（Internet Explorer 不支持 meter 标签）
<progress>：定义运行中的进度（进程）。
```