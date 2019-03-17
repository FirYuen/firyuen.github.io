---
title: JS里的类型
date: 2018-06-18 14:42:11
tags:
---

1. ##### 目录

   - 类型转换
   - 各类型的API
   - 内存图
   - 深复制

2. ##### 类型转换

   - 转字符串string（比调用toString()API更常用简单的方法）

     - 使用`+''`或者`''+`（即与空字符串相加）

       ```js
       1 + ''
       "1"

       true + ''
       "true"

       var obj = {}
       obj + ''
       "[object Object]"

       null + ''
       "null"

       undefined + ''
       "undefined"

       //+ ''的逻辑是如果发现左右任意一边有字符串，它就会尝试把另外一边也变成字符串；+号总是希望能得到两个字符串。
       ```

     - 一个问题`1+'1'=?`

       解答:由于加号只能加相同类型的东西，所以它会尝试改变这个类型，**优先会尝试把数字变成字符串**，所以上面的的问题可以等价于`(1).toString()+'1'`所以结果是`'11'`

   - 转布尔值boolean（比Boolean()全局方法更常用简单）

     - 用`!!`给任何东西取反两次就会得到一个布尔

       ```js
       !true   //取反一次
       false
       !!true	//取反两次，根据这个得出新的方法，用任何东西给它取反两次就会得到一个布尔
       true	

       !! 1	//number
       true

       !! 0	//number 0  false
       false

       !! ''	//空字符串   false
       false

       !! '  ' //非空字符串  
       true

       !! {}   //空对象
       true

       !! {name: 'xiao'}   //非空对象
       true

       !! null			 //null  false
       false 

       !! undefined      //undefined  false
       false 
       ```

     - JS里面其它的值变成布尔的时候，只有**五个**特殊值（七种数据类型，symbol先不考虑剩下的六种,布尔变布尔false变false除外），number里面只有两个是false分别是`0`和`NaN`;string里面只有一个是false，只有空字符串`''`;`null`只有一个值,它就是false；`undefined`也只有一个值，它是false;所有的object都是true包括数组跟函数.

       ```js
       !! 0     //数值0
       false
       !! NaN   //数值NaN
       false
       !! ''    //空字符串
       false
       !! null  //null
       false
       !! undefined  //undefined
       false
       //上面五个是 五个falsy(adj:假的,假值)值!
       ```

     - 关于falsy值,falsy是在 Boolean 上下文中认定可转换为false的值;JavaScript在需要用到布尔类型值的上下文中使用强制类型转换将值转换为布尔值，比如：在条件语句或者循环语句中.

       ```js
       if (false)
       if (null)
       if (undefined)
       if (0)
       if (NaN)
       if ('')
       if ("")
       if (document.all) [1]
       //严谨来说有上面8个
       ```

   - 转number（把其它数据类型转成number）五种方法

     * `Number('1') === 1`

     * `parseInt('1',10) === 1`全局函数，把它变成整数，第二个参数表示进制，一般都要加上，如果没加上表示默认10进制.

     * `parseFloat('1.23') === 1.23`把它变成浮点数，不用写第二个参数，因为它只有10进制。

     * `'1'-0 === 1` 减0，任何一个东西减上一个0都会得到一个number，既有`parseInt`的功能也有`parseFloat`的功能，所以最常用。

       ```js
       '1'- 0
        1                 //减0
       '1.23' - 0
        1.23              //减0
       ```

       但是上面的方法没有`parseInt`和`parseFloat`严谨,遇到特殊情况结果不同，如下图：![](http://p0mf9ztbm.bkt.clouddn.com/17-12-17/59014222.jpg)![](http://p0mf9ztbm.bkt.clouddn.com/17-12-17/66054381.jpg)

       ​

     * `+ '1'=== 1`取正，`+`表示取它原本的值用数字表示。

       ```js
       + '1'
       1                 //取正，不是绝对值
       + '.1'
       0.1               //取正
       + '-1'
       -1                //取正
       -(- '-1')
       -1                //拓展，取-('-1')的负数
       ```

       图示：![](http://p0mf9ztbm.bkt.clouddn.com/17-12-17/74849596.jpg)

       一般常见的面试考点都是考第二种`parseInt`例如：

       ```js
       parseInt('011')
       11                       //以前结果是9，因为0开头会被认为是8进制
       parseInt('011',8)
       9                        //8进制
       parseInt('011',10)
       11                       //10进制
       一些奇怪的考点:parse会从头开始能parse多少就parse多少，（这也是与减0跟取正不同的地方）一旦不能parse它就返回。
       parseInt('sss')
       NaN                     //不存在的数字
       parseInt('1s')
       1                       //后面s不能parse了返回1
       parseInt('12s')
       12                      //后面s不能parse了返回12
       ```

3. ##### 各类型的API

   - 转成string的API`toString()` 以及用String的全局方法`window.String()`

     - 如果想让一个东西变成字符串，如果它能变成字符串,调用下toString就行。

     ```js
     var n = 1
     n.toString()
     //"1"     number转string

     var b = true
     b.toString()
     //"true"  boolean转string

     var a = null
     a.toString()
     // null转string语法错误，`Uncaught TypeError: Cannot read property(属性) 'toString' of null`,null没有toString这个API。

     var c = undefined
     c.toString()
     //undefined转string语法错误，`Uncaught TypeError: Cannot read property 'toString' of undefined,同样的，undefined没有toString这个API。

     var object = {name:'xiao'}
     object.toString()
     // "[object Object]" 有toString这个API，不过结果不是我们想要的，得到的是"[object Object]"，前面小写，后面大写。
     ```

     - `console.log`其实也是用的上面的原理，理论上console.log只能接受字符串，console.log如果发现不是字符串就会调用toString函数，也叫做API。除了console.log很多其它的地方也会如此。

     ```js
     console.log('xiao')
     xiao
     //出来的结果没有引号包裹xiao，是因为浏览器打出的东西是瞎打的，

     console.log(1)  //相当于console.log((1).toString())
     1
     //虽然没加引号，其实是浏览器省略了。

     var obj = {}
     obj['name'] = 1  //object默认的key是字符串，给的'name'也是字符串，所以打印出来是1。
     //1
     //obj{name :1}

     obj[2] = 2		//但是如果直接给obj一个数字为2的key，它会默认把数字2toString()成字符串，所以
     //2				能打印出来2，obj里面也增加了一个字符串2的key。
     //obj{2: 2, name: 1}

     obj[true] = 3		//给一个布尔为true的key也是同样的道理，console.log会默认把true转成字符串
     //3					 true。
     //obj{2: 2, name: 1, true: 3}   //现在obj有三个key了，除了字符串'name'，数字2跟布尔true都是								   自动转换的。

     obj[{}] = 4
     //4
     //obj{2: 2,name: 1,true: 3,[object Object]:4}  //道理同上，这里换成了对象调用toString()
     ```

     - `window.String()`示例这个跟加号的功能一样强大,它是一个全局函数

     ```js
     window.String(1)              //number
     "1"

     window.String(true)			 //boolean
     "true"

     window.String({})			 //object
     "[object Object]"

     window.String(null)			 //null
     "null"

     window.String(undefined)	 //undefined
     "undefined"
     // window.可以省略
     ```

   - 转成boolean的全局函数`Boolean()`要大写开头

     - 下面示例

     ```js
     Boolean(1)
     true
     Boolean(2)
     true
     Boolean(0) //number 0，结果是false
     false

     Boolean('') //空字符串,结果是false
     false
     Boolean(' ') //空格字符串
     true  
     Boolean('1') //其它字符串都为true，因为里面有东西
     true

     Boolean(null)  //null，结果是false
     false

     Boolean(undefined) //undefined，结果是false
     false

     Boolean({})  //空对象，结果是true
     true
     Boolean({name:'xiao'}) //只要是对象，结果都是true
     true
     ```