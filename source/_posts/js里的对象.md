---
title: js里的对象
date: 2018-06-18 14:50:58
tags:
---

##### 什么是标准库?

* js的内存里面有两种东西，一个是stack（栈内存），一个是heap（堆内存），stack里面有个特别重要的变量叫做global，在浏览器里面叫做window，他们是一样的都是同一个对象。window是一个对象，window就对应heap里面一块内存，window是一个哈希表，哈希表里面的东西分两部分，一部分就叫做**标准库**，另一部分叫做非标准库。

* 标准库包括哪些呢？比如Object()函数，这个函数也是个对象，它有一个key()属性，create()方法；还有String()函数，Nubmer()函数，Array()函数，Boolean()、Function()。

  图示:![](http://p0mf9ztbm.bkt.clouddn.com/17-12-8/11523085.jpg)

##### 简单类型跟复杂类型加new与不加的区别

* 给Object传什么它就会把它包装成一个什么对象,传给它一个1就把1包装成Number对象，给它一个字符串就包装成一个字符串对象，如果什么都不给就会生成一个空对象；对于Object来说加不加new都一样。如下图：![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/33582031.jpg)

* String是将给的东西变成一个字符串常量（非对象，基本类型），如果加new就会生成String对象如下图：![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/12214723.jpg)

* Number与String同理，给Number一个不能变成数字的东西变成NaN，给一个可以变的变成number常量，如果加了new就会返回一个number对象。如下图：![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/90343838.jpg)

* Boolean会把提供的任何东西变成一个布尔值，另外记住5个falsy值(0、NaN、''、null、undefined)，new Boolean则会返回一个Boolean 对象如下图:![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/11213113.jpg)

* 所以除了Object加或者不加new没区别，其余的类型加new都会返回一个相应的对象。

* ##### **总结**，全局变量分两种，一种是对应的原本是七种数据类型中的基本类型（number、string、boolean）（null、undefined没有构造函数）；另一种跟对象相关的obejct（包括两种特殊的obejct，array和function）；如果是基本类型对应的构造函数，加new与不加new的区别就是，不加new的时候返回一个基本类型，如果加了new返回一个复杂类型（对象）；如果是object复杂类型，加new不加new是一样的。都返回一个对象。![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/4291338.jpg)

##### 新的API  Array

Array是一个构造数组的**全局对象**(七种数据类型Nubmer、String、Boolean、Symbol、null、undefined、Object[Array、Function])

**创建数组：**

```js
let f = ['a','b']
let f = new Array('a','b')   //两种写法等价
```

**Array构造函数的两种用法：**一个或者多个参数

```js
var a = Array(3)
//生成一个长度为给的数字(3)的数组，不含0,1，2，有三个undefined，第一个参数是长度
var a = Array(3,3)
//当是一个参数的时候，第一个参数是长度，当有两个参数的时候，第一个参数不是长度，它是第一项
```

***

首先第一种用法`var a = Array(3)`，它会生成一个长度为3，每一个都是undefined的数组a[0]是undefined，a[1]是undefined，a[2]也是undefined；但是又不在a里面，也就是说a没有012，这时候最好画内存图，在研究数据的时候最好的方式就是画内存图。

**console图**如下：

![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/55013552.jpg)

**内存图**演示，当写`var a = Array(3)`的时候到底做了什么，在stack里面声明了一个地址，a指向这个地址（ADR99），heap对应的ADR99里面存了一个`length:3`以及一个`__proto__ `指向`Array.prototype`（Array的公有属性）；也就是说当写`var a = Array(3)`的时候它生成了一个对象，这个对象里面写了一个`length:3`以及`--proto`指向公有属性（Array.prototype），公用属性里面还包括一些`push`、`shift`之类的函数。0，1，2，3并没有存到heap对应的ADR99中。内存图解如下：

![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/21878716.jpg)

再来重新看代码`a.length // 3`对应上图中的`length:3`,`a.push`函数也是存在的，因为可以在公用属性`__poroto__`找到，可以通过`console.dir(a)`把a打印出来。a的第一层只有`length: 3`以及`__poroto__:Array(0)`指向的一个哈希函数（`a.__proto__`等于等于`Array.prototype`(Array构造它的函数)）![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/11724928.jpg)

***

第二种用法`var a = Array(3,3)`，当有两个参数的时候，第一个参数不是长度，它是第一项

如图：![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/5351149.jpg)

***

所以`var a = Array(3)`和`var a = Array(3,3)`对应的东西并不相同，同样是3，同样的位置，同一个函数却因为参数个数不同而不相同，这叫做JS的不一致性，这也是JS的缺点所在如图：![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/32443819.jpg)



***

由于Array也属于Object，所以Array加不加new并没有区别。![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/17324027.jpg)

##### Function

类比array的`var a = new Array(1,2,3)`与`var a = [1,2,3]`写法function也有可有有下面两种写法。

```js
var f = function(a,b){
    return a+b
}  // f(1,2) 返回3
//上面可以用它的构造函数构造出来
var f = new Founction('a','b','return a+b')  //f(1,2)同样返回3
```

函数有参数，必须有返回值`return a+b` 同时可以用它的构造函数构造出来。先传一个字符串表示**第一个参数**				 名字，再传一个字符串表示**第二个参数**名字，最后传一个字符串表示**函数体**`'return a+b'`

new Function的用法就是把所有东西变成字符串依次排开

```js
var f = new Function('a','b','return a+b')
```

*MDN语法*

```js
new Function ([arg1[, arg2[, ...argN]],] functionBody)
//用[]标的叫做可选，意思是可以只传一个参数，两个参数或者N个参数，也可以不传参数只传函数体，另外加不加new没区别。
```

##### Function与function的区别

* function是关键字，是函数的意思，没有任何意义，同样的关键字还有(var、if、else等等)，下面举例

  ```js
  var  //声明一个变量
  var a = 1  //声明一个a，a不一定是函数
  function //声明一个函数
  function f(){} //声明一个f，f一定是个函数
  ```

* Function是一个全局对象

  ```js
  window.Function
  window.Object
  ```

* 七种基本类型（number、string、boolean、symbol、null、undefined、object）的大小写无所谓，因为它们只是一个字符串，例如字符串它的英文是`string`用大写`String`表示也可以仅此而已。举例声明一个string

  ```js
  var s = new String()   //因为没有小写string这个关键字，所以用String，
  ```

  ![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/48534517.jpg)

  同理function就是表示函数的意思关键字，跟代码没有任何关系。声明函数必须用`function f`

* 声明一个函数的两种方法，function跟Function都可以，记住分别怎么用就行了。

  ```js
  function f(){}
  var f = new Function('x','y','x+y')  //用一个变量去引用一个对象，另外new可以省略。
  ```

* 声明函数的几种方法

  ```js
  具名函数 
  function f(x,y){      //x,y是参数，可以没有
  	return undefined  //一定要有return，就算不写也会自动加一个undefined
  }
  匿名函数 
  function (){
       return
  }
  Funtion                //一般不用这个方法
  new Function('x','y','x+y')
  //前两种用关键字声明函数，最后面的是用全局对象在声明一个对象函数.
  ```

* 拆解

  ```js
  var a = 1 //变形成成下面
  var a
  a = 1

  var f = function(){}//变形成下面,所以这是两句话,声明函数只有上面两种方法(关键字和new Function)
  var f   //先去声明一个f变量
  f = function(){}   //然后让f等于一个匿名函数,内存图如下
  ```

  ![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/256795.jpg)

  如果现在让f=1那么就会将stack里面的A88地址擦掉换成1,中间的联系就会断掉,但是函数function(){}还在,f跟function没有任何关系.`var f = function(){}`是两步,一步是弄一个变量`f`一步是弄一个对象`function(){}`然后将它们联系起来,所以`var f = function(){}`不是一个语法,声明函数只有上面两种方法(关键字和new Function)![](http://p0mf9ztbm.bkt.clouddn.com/17-12-9/98458059.jpg)

* 具名函数跟匿名函数的区别

  具名函数一步做到初始化然后赋值,匿名函数是先声明一个变量`f`,然后再弄一个匿名函数,然后把变量`f`指向`function (){}`分两步.

  ***

  ##### 数组&a.forEach

  ​
