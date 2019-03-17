---
title: CSS-1
date: 2018-05-19 14:28:07
tags:
---

 
## CSS 的历史

[中文维基百科](https://zh.wikipedia.org/wiki/%E5%B1%82%E5%8F%A0%E6%A0%B7%E5%BC%8F%E8%A1%A8#.E5.8E.86.E5.8F.B2 "null")
[英文维基百科](https://en.wikipedia.org/wiki/Cascading_Style_Sheets#History "null")

注意中文维基百科严重落后了。

1.  两个人合作发明了 CSS
    1994年哈肯·维姆·莱提出了CSS的最初建议。伯特·波斯（Bert Bos）当时正在设计一个叫做“Argo”的浏览器，他们决定一起合作设计CSS。
2.  W3C 开始接管 CSS
    1997年初，W3C内组织了专门管CSS的工作组，其负责人是克里斯·里雷。
3.  CSS 2.1
    1998年5月W3C发表了CSS2
    CSS2.1修改了CSS2中的一些错误，删除了其中基本不被支持的内容和增加了一些已有的浏览器的扩展内容。
4.  CSS 3
    从 2011 年开始 CSS 被分为多个模块单独升级，统称为 CSS 3。这些模块有：
    *   CSS 选择器 level 3
    *   CSS 媒体查询 level 3
    *   CSS Color level 3
    *   更多请 [搜索 CSS spec](https://www.google.com/search?q=css+spec&oq=css+spec&aqs=chrome..69i57j69i60l5.1235j0j7&sourceid=chrome&ie=UTF-8 "null")
5.  CSS 4?
    不好意思，没有 CSS 4，只有各个模块的 level 4

周边工具

*   LESS CSS
    一种简化、功能更多的 CSS 语言 [中文官网](https://www.google.com/search?q=less+css+%E4%B8%AD%E6%96%87 "null") [英文官网](https://www.google.com/search?q=less+css "null")
*   SASS
    一种简化、功能更多的 CSS 语言（请自行搜索中英文官网）
*   PostCSS
    一种 CSS 处理程序

我的建议是，先不要看周边工具，学好最朴素的 CSS，然后升级就很容易了。

## CSS 学习资源

1.  Google: 关键词 MDN
2.  [CSS Tricks](https://css-tricks.com/ "null")
3.  [Google: 阮一峰 css](https://www.google.com/search?q=%E9%98%AE%E4%B8%80%E5%B3%B0+css "null")
4.  [张鑫旭的 240 多篇 CSS 博客](http://www.zhangxinxu.com/wordpress/category/css/page/25/ "null")
5.  [Codrops 炫酷 CSS 效果](https://tympanus.net/codrops/category/playground/ "null")
6.  [CSS揭秘](http://www.ituring.com.cn/book/1695 "null")
7.  [CSS 2.1 中文 spec](http://cndevdocs.com/ "null")
8.  [Magic of CSS](http://adamschwartz.co/magic-of-css/ "null") 免费在线书

我的建议是：中文学习资源只看大 V 的（毕竟他们要维护形象不能瞎写），英文资源看 CSS Tricks、MDN 和 Codrops。书的话作用不大，最权威的书其实是文档。

*   如果你想快速上手，就先写小 demo 再学理论。
*   如果你想一鸣惊人，就仔细看 CSS 规范文档。

## 开始写 CSS

1.  引入 CSS 的三/四种方式
2.  从最小的东西开始入手
3.  逐渐变大
4.  学会组织 CSS（以后再说）
5.  自己写 CSS UI 库


    ## CSS 代码

    ## 知识点

    1.  如何做横向布局（float + clearfix）
    2.  如何取色、量尺寸、预览字体（Word）
    3.  如何使用开发者工具查看样式、继承样式
    4.  四种引入 CSS 的方式：style 属性、style 标签、css link、css import
    5.  常见 CSS 属性：
        1.  font-family font-size font-weight
        2.  ul、body 的默认 margin 和 padding
        3.  color、background-color、margin、padding
        4.  line-height

## CSS 全称是什么
- Cascading Style Sheets   

## 不会 CSS 里面的 transform 属性，最应该搜什么关键词？
- CSS transform MDN

## CSS 里，为什么 color: red 可以让文字变红色？
- 因为浏览器看到 color: red 就会将对应的文字变红
- 具体原理要看浏览器代码，但是目前我看不懂浏览器代码
- CSS 是一种声明式语言，只需要写出对应的声明，就会产生对应的效果
- 因为 color 表示文字颜色，red 表示红色。

## 预期上、下、左、右内边距分别 1px 2px 3px 4px，那么下面写法正确的有：
- padding-top: 1px; padding-bottom: 2px; padding-left: 3px; padding-right: 4px;
- padding: 1px 4px 2px 3px;

## .xxx {text-align: center;} 的作用是？
- 让 .xxx 子代中的内联元素居中

## 我需要一个 div 高度为 30px，div 里有一行字垂直居中，字的大小为 14px，应该怎么写 CSS?
- 给 div 的样式为 font-size: 14px; line-height: 20px; padding: 5px 0;
- 给 div 的样式为 font-size: 14px; line-height: 24px; padding: 3px 0;
- 给 div 的样式为 font-size: 14px; line-height: 30px; //这个比较奇特,设置了行高之后,文字就会自动垂直居中

## 方方说用 float 做横向结构需要做哪两件事？
- 给所有子元素加 float: left 2. 给父元素加 clearfix 类

```css
.clearfix::after {
    content: '';
    display: block;
    clear: both;
    
}
```