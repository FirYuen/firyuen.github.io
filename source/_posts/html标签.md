---
title: html标签
date: 2018-05-18 19:41:12
tags:
---

## `<iframe>` 和 `<a>` 标签
    ```javascript
    <iframe src="https://www.baidu.com" name="xxx"></iframe>
    <a href="" target="xxx"></a >
    ```
    `<iframe>`元素用于在当前网页嵌套页面,`<iframe>`最好少用了
    `frameborder=0`用来消除默认边框
    
    ### `<a>`标签target
    |标签|含义|
    |-|:-:|
    |_blank	|在新窗口中打开被链接文档。|
    |_self	|默认。在相同的框架中打开被链接文档。|
    |_parent	|在父框架集中打开被链接文档。|
    |_top	|在整个窗口中打开被链接文档。|

    ### `<a>`标签的download属性可以下载
## `<a>`的href
    href后加http://qq.com会打开链接,直接加qq.com则不会
            加`//`就会用当前的协议打开连接
            加`#`会到指定锚点 只有锚点是不发请求的,只在当前页面跳转
            加`?name=xxx`浏览器会自动帮助发起请求
            加`javascript: alert(111);` 直接执行js代码
            加`javascript:;` 一个`<a>`连接,点击后什么也不执行 
            href为空点击则刷新自身

## `<form>`一般用来post内容
    ```html
    <form action="index2.html" method="post">
        <input type="text" name="username">
        <input type="password" name="password">
        <input type="submit" value="提交">
    </form>
    ```

## `npm install http-server`
    alias hs
    http-server -c-1 则不会缓存

## input的[属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input)
## button的[属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/button)
    1. 如果一个`<form>`中只有一个`<button>`,这个button会自动升级为submit,但是如果给button指定type,那么这个表单就没有提交按钮
    2. 如果`<form>`中有一个`<input>`,它的type是submit,也达到submit的效果
    3. 如果需要输入完成后按enter提交,需要submit属性

## `<label>`是为了与input结合绑定的,按下`<label>`标签内容,到输入框
    ```html
    <label for = "username">用户名</label><input type = "text" name = "username" id = "username">
    <input type = "checkbox" id = "xxx"><label for = "xxx">你好</label>
        //label是为id为xxx准备的,此时按你好也能勾选
        //骚操作,以下也是同样效果
       <label >用户名<input type = "text" name = "username"  id = "username"></label>
    ```
## `<input>`都要加name属性,否则服务器无法读到
    `checkbox`可以自己指定value,name相同成为同一类,可以勾选多个//多选框
    `radio`可以自己指定value,name相同成为同一类,只能选中一个//单选框

## `<select>`
    ```html
<select name="group" id="" multiple>//alt键多选
  <option value="">-</option> //空组
  <option value="1">1</option>
  <option value="2">2</option>
  <option value="3" disabled>3</option> //禁止选中
  <option value="4" selected>4</option> //默认选中
</select>
    ```
## `<textarea>`
    ```html
    <textarea style="resize: none" name="hobby" id="" cols="30" rows="10"></textarea> 
    //cols列 rows行,只能大概控制,具体控制大小用css
    //禁止用户改变文本输入区域大小
    ```