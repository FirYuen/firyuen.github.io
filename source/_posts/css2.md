---
title: CSS-2
date: 2018-05-19 23:21:40
tags:
---
* 1.文档流
    文档流的英文是 Normal Flow,文档流代表元素在文档中的「流动」方向, `float:left`、`position:fixed`、`position:absolute` 都能使元素脱离文档流

* 2.浏览器会给`<body>`加默认样式
    感觉最好这么搞:
    ```css
    body{
        margin:0px;
        padding:0px;
    }
    ```
* 3.高度是由什么决定的
    1.  内联元素
    `line-height`
     给`内联元素` 元素设置宽高是无效的,给`内联元素`元素设置 margin-top margin-top 是无效的
    2.  块级元素
    块级元素的高度由其内部文档流元素的高度总和组成
    `<div>`如果有boder在流动过程中被截断,则只会显示一半,单词太长会直接被换行`word-break:break-all`可以解决这个问题

* 4.position 的 5 个取值
    A. sticky
    B. absolute
    C. fixed
    D. relative
    E. static
* 5.字体默认的 line height 由字体设计师决定

* 6.子元素会继承父元素样式

* 7.`content-box` 与 `border-box` 的区别是 `border-box` 的 `width` 包括 `padding` 和 `border`

* 8. CSS 盒模型Block box与Line box
    `display ： block` 、 `list-item` 以及 `table` 会让一个元素成为块级元素。
    正常流中，块级元素框的水平部分 = 其父元素的width = margin-left+margin-right + padding-left+padding-right+ border-left+border-right+自身width
* Line Box

每一行称为一条Line Box，它又是由这一行的许多inline-box组成，它的高度可以直接由line-height决定，line boxes的高度垂直堆叠形成了containing box的高度，就是我们见到的div或是p标签之类的高度了。

## 基础概念

### 匿名文本

<code><div>当你只有一把锤子<span>一切看起来</span>都像是颗钉子</div></code><code>未包含在行内元素的字符串（当你只有一把锤子，都像颗钉子）就叫匿名文本</code> 
### 内容区 行内框 间距

![clipboard.png](https://segmentfault.com/img/bVvMvz "clipboard.png")

###内容区
css假设每个元素都会生成一个或者多个Box，称为元素框，元素框中心有内容区，内容区外周围包括了padding，border，margin，但是，替换元素是包括外边距，内边距，边框的。
###行间距
行间距是font-size与line-height的差值，被分成两半在内容区的上下
###行内框
非替换元素，行内框高度=line-height
替换元素，行内框高度=内容区宽度（行间距不应用到替换元素）
###行高
两行文字基线的距离
###行框
一行有很多行内框，行框是包含这一行行内框最高点和最低点的
###基线
不同元素的基线位置不同，整个行框会有一个基线，行内元素的位置是基于两者基线对齐

### vertical-align(垂直对齐)
```
    该属性 定义 行内元素的基线相对于该元素所在行的基线的垂直对齐的方式。
    只有一个元素属于inline或是inline-block（table-cell也可以理解为inline-block水平）水平，其身上的vertical-align属性才会起作用.
    同时也可以知道，改变其，会影响到行内框的位置，从而会影响到一整行行内元素的位置
```
需要注意vertical-align为数值时，会让文字上下移动，当其为百分比时是针对font-size的百分比

### line-height（行高）

```html
<div style="width:100px;height:10px"></div>
//这个div调整line-height不会发生变化，因为里面没有文字
<span style="line-height:10px;border：1px solid green"></span> 
//span的高度会随着line-height的变化而变化
//说明行内元素的高度是由line-height的支撑决定，行内框的高度也等于line-height</code>
```
### 管理line-height

因为line-height是根据自己font-size设置，而不是父元素，所以将line-height设置为1em,该元素的line-height则会与相同（em单位是一般是相对与父元素进行设置大小）
```html
<div style="font-size:12px;line-height:12px">
    <span style="font-size:15px;line-height:1em">
        嘿嘿嘿，这里的line-height值为15px
    </span>
</div>
```
### margin padding border对行高的影响

*   行内元素其padding、margin、border-top、border-bottom 不会增加行高。
    padding会覆盖；margin将重置为0；border-top和border-bottom同样会覆盖。

![clipboard.png](https://segmentfault.com/img/bVvMHG "clipboard.png")

*   css2.1规定margin-top和margin-bottom可以运用到不是行内非替换元素的所有其他元素

*   行内替换元素（如：img）元素会影响行高

### inline-block
将对象呈现为inline对象，但是对象的内容作为block对象呈现。之后的内联对象会被排列在同一行内。
比如我们可以给一个link（a元素）inline-block属性值，使其既具有block的宽度高度特性又具有inline的同行特性。

<br>
<hr>
# 参考资料
[《CSS 权威指南 第三版》](http://www.cnblogs.com/rainman/archive/2011/08/05/2128068.html)
[《The Definitive Guide to Using Negative Margins》](http://www.w3cplus.com/css/the-definitive-guide-to-using-negative-margins.html)
[margin为负值产生的影响和常见布局应用](http://www.jianshu.com/p/549aaa5fabaa)
[CSS布局 -- 圣杯布局 & 双飞翼布局](http://www.cnblogs.com/imwtr/p/4441741.html)
[CSS深入理解vertical-align和line-height的基友关系](http://www.zhangxinxu.com/wordpress/2015/08/css-deep-understand-vertical-align-and-line-height/)
[深入理解CSS中的行高](http://www.cnblogs.com/rainman/archive/2011/08/05/2128068.html)
[想要清晰的明白（二）CSS 盒模型Block box与Line box](https://segmentfault.com/a/1190000005155084)