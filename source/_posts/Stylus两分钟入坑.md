---
title: Stylus两分钟入坑
date: 2019-01-20 13:07:33
tags:
---
下面中规中矩的CSS代码是否看得眼睛生茧了？
```css
body {
  font: 12px Helvetica, Arial, sans-serif;
}
a.button {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
```
好，去掉花括号
```css
body
  font: 12px Helvetica, Arial, sans-serif;

a.button
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
```
去掉分号
```css
body
  font: 12px Helvetica, Arial, sans-serif
  
a.button
  -webkit-border-radius: 5px
  -moz-border-radius: 5px
  border-radius: 5px
```
还有你冒号
```css
body
  font 12px Helvetica, Arial, sans-serif
  
a.button
  -webkit-border-radius 5px
  -moz-border-radius 5px
  border-radius 5px
```

来点函数
```css
border-radius()
  -webkit-border-radius arguments
  -moz-border-radius arguments
  border-radius arguments
  
body
  font 12px Helvetica, Arial, sans-serif
  
a.button
  border-radius(5px)
```
加点混合书写
```css
border-radius()
  -webkit-border-radius arguments
  -moz-border-radius arguments
  border-radius arguments
  
body
  font 12px Helvetica, Arial, sans-serif
  
a.button
  border-radius 5px
```
加点模块化
```css
@import 'vendor'

body
  font 12px Helvetica, Arial, sans-serif
  
a.button
  border-radius 5px
```
甚至是语言函数
```css
sum(nums...)
  sum = 0
  sum += n for n in nums
  
sum(1 2 3 4)
// => 10
```
好了，你得到了Stylus
