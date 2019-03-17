---
title: 背景图片虚化css
date: 2018-11-16 12:33:54
tags:
---
#记录一下css的背景图片虚化模糊的样式

```html
<body>
<div class="cover">
  你好
</div>
</body>
<
```
```css
.cover{
  width:400px;
  height:400px;
  border:1px solid red;
  position:relative;
}
.cover::after{
  content:'';
  position:absolute;
  top:0;
  left:0;
  width:100%;
  height:100%;
  background: transparent url(http://p1.music.126.net/_ZIyHUML8sXBvJXqLdQDOg==/105553116278617.jpg?imageView&thumbnail=360x0&quality=75&tostatic=0) no-repeat center;
  filter:blur(5px)
}
```
