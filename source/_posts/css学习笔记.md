---
title: css学习笔记
date: 2018-05-21 23:42:38
tags:
---
*   一个元素的高度是由内容决定的，不要给他设定确定的高度。div高度由其内部文档流元素的高度总和决定，并不是相等，只是决定。
*   文档内元素的流动方向叫文档流
*   内联元素从左往右流，如果遇到宽度不够的阻碍，再另起一行继续流，如果是块级元素，每个块占一行，从上往下一直流。
*   添加border是很方便的调试方法。
*   如果内联元素是个很长的单词，默认情况下是不能分开的。如果要打破需要添加`word-break`属性。

*   `word-break`属性取值举例`break -all` 、`break-word`


*   内联元素的高度（难点）

    *   文字的居中不是让文字的中线居中对齐，而是让基线对齐。

        上图对齐蓝色的小a才是正确的。

        上面中间的箭头就是基线、上下分别是上下线，中间的虚线叫中线。

    *   每种字体的浏览器默认建议行高不一样。具体情况是由设计师给的字体`font-size`大小然后在不同的字体情况下有不同的建议行高。
    *   多个span在一起的时候，这一行的高度则由最高的span决定。

    *   内联元素的高度基本是不可测的，在font-size比较小的时候可以用`line-height`来控制内联元素所占的高度，如果想要一个特定的高度，可以再在基础上添加padding来增加。

```css
	div{
          border: 1px solid green;
          line-height:24px;
          padding:6px 0px;
        }
        /**上面最后div的高度近似于40px**/
```
*   脱离文档流:一旦脱离文档流，那么父元素的高度则不受该文档控制，父元素会自动忽略他。

    *   `position fixed`相对于屏幕
       
```css
	.topNavBar{
            position: fixed;
            top: 0;
            left: 0;
        }
        /**相对于屏幕左上角固定**/
```
<br>

 如果是fix定位，元素的宽度不会拓展，会往内缩，这时候一般设置`width:100%`但是给当前div设置100%因为它本身有一个padding宽度，再加上width:100%会超过其父元素，可以通过给要设置的div里面再添加一个div然后给这个新增的div增加padding。
<br>

*   绝对定位，在子元素写position:absolute;在父元素写position:relative;
    ```css
		div{
            position: absolute;
            left: 4px;
            top: 100%; /**离父元素100%的距离，从左往右4px的距离。**/
        }
	```

*   设置`display:inline block;`后，外边距`margin`不会合并。

*   随便加`padding`，不行就加`margin`

*   做半透层背景：`background-color: rgba(0,255,0,0.8)`;/**不要颜色（黑色），半透层背景**/

*   背景图片居中：`background-position: center center;`

*   背景图片按比例缩放：`background-size: cover;`

*   不要设定固定的宽度，可以设置最大宽度,如果屏幕比最大宽度小可以自适应:`max-width:940px;`
*   div设置水平居中
```css
margin-left:auto;
margin-right:auto;
```
*   span等内联元素不接受宽高，设置也没用，必须设置`display:inline-block;`
```css
.userCard .welcome{
      background: #E6686A;
      color: white;
      display: inline-block;
      width: 70px;
      height: 29px;
      line-height: 29px;
      text-align: center;
    }
    /**上面的做法一般是新手做法，虽然一般情况下（line-height不高的情况下）设置line-height与height高度相等会居中，但是实际line-height会与设定的值不一样，而且会产生bug**/
```
*   上面的代码块的效果可以通过下面方法完成，从内像外做,先测原效果宽高为70 30 现有宽高是40 20，宽度现在差30左右给15pxpaading，高度差10上下给5pxpadding。
```css
.userCard .welcome{
        background-color: #E6686A;
        color: white;
        display: inline-block;
        padding: 5px 15px;
          line-height: 20px;
        
    }
    
    <!-- /**这种效果比上面还具有一种优势，无论span里面的内容(welcom)增加或减少，居中都不会变。**/
    /**需要注意的事最后还要添加line-height:20px;尽管现在在机器上是20px了，但是有些机器可能会变动，添加line-height之后可以明确表明20px+2*5px=30px**/  -->
```
这两块CSS的HTML代码为`<span class="welcome">Hello</span>`

*   用CSS画一个三角形 推荐网站：[https://css-tricks.com/examples/ShapesOfCSS/](https://css-tricks.com/examples/ShapesOfCSS/ "null")
```css
div{
      border: 100px solid transparent;
      width: 0px;
      border-left-color: #E6686A;
      border-top-width: 0px;
    }
    /**可以先画出一个10px solid red的border 给div宽高设为10X10，然后设置四边border颜色慢慢演化，忘了就自己再做一遍。**/
    /* transparent 透明是个好属性。 */
```
*   span里面设置`display:block;`就相当于div
*   float元素默认会收缩
*   hr线
```css
hr{
        height: 0;
        border:none;
        border-top: 1px solid #DEDEDE;
    }
    .userCard .text hr{
        margin: 20px 0px;
    }
```
*   dl浮动套路
```css
.userCard dl dt,
    .userCard dl dd{
        float: left;        /**逗号分隔，表示两个都遵循float浮动**/
    }
    .userCard dl dt{
        width: 30%;
    }
    .userCard dl dd{
        width: 70%;         /**利用浮动自动换行的特性左边width30%,右边width70%**/
    }
```
*   svg语法记住三个
```css
svg{
        width: 30px;
        height: 30px;
        fill: white;
        vertical-align: top;  /**缩小下边距**/
    }
```
*   a标签搭配svg
```css
a{
        display: inline-block;
        border-radius: 50%;      /**圆形**/
        width: 40px;
        padding: 5px 0;          /**不要设置高度，容易出bug**/
        line-height: 30px;
        margin: 16px 16px;
    }
    /**习惯加border调试**/
```