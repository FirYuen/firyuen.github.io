---
title: 'JavaScript中call(),apply(),bind()用法的理解'
date: 2018-11-10 14:49:28
tags:
---
其实做题时并不了解这三个方法的用法,但是稍微学习了一下,网上的资料很丰富,马上就知道了,记录下,做个备忘.

##### 例1
    ```JavaScript
var name = '张三',age=20;
var obj={
    name:"李四",
    objAge:this.age,
    myfun:function(){
        console.log(this.name+"年龄"+this.age);
    }
}

obj.objAge //20
obj.myFun() //李四年龄undefined
    ```

##### 例2
    ```JavaScript
var name = "张三";
function getName(){
    consol.log(this.name);
}

getName() //张三
    ```
比较一下这两者this 的差别，第一个打印里面的this 指向obj，第二个全局声明的getName()函数this 是window ；

1. ##### call()、apply()、bind() 都是用来重定义 this 这个对象的！

##### 如:
```JavaScript
var name = "张三",age= 20;
var obj={
    name:"李四",
    objAge:this.age,
    myfun:function(){
        console.log(this.name+"年龄"+this.age);
    }
}
var obj2={
    name:"王二",
    age:40
}

obj.myFun.call(obj2)；　　　　//王二年龄40
obj.myFun.apply(obj2);　　　 //王二年龄40
obj.myFun.bind(obj2)();　　　//王二年龄40

```
以上出了bind 方法后面多了个()外 ，结果返回都一致！由此得出结论，bind() 返回的是一个新的函数，你必须调用它才会被执行

2. ##### 对比call(),apply(),bind()传参的情况下
```JavaScript
var name = "张三",age= 20;
var obj={
    name:"李四",
    objAge:this.age,
    myfun:function(fm,t){
        console.log(this.name+"年龄"+this.age,"来自"+fm+"去往"+t);
    }
}
var obj2={
    name:"王二",
    age:40
}

　　obj.myFun.call(obj2,'成都','上海')；　　　　 //王二 年龄 40  来自 成都去往上海
　　obj.myFun.apply(obj2,['成都','上海']);        //王二 年龄 40  来自 成都去往上海  
　　obj.myFun.bind(obj2,'成都','上海')();         //王二 年龄 40  来自 成都去往上海
 　  obj.myFun.bind(obj2,['成都','上海'])();　　 //王二 年龄 40  来自 成都,上海去往undefined

```

##### 从上面四个结果不难看出
 - call 、bind 、 apply 这三个函数的第一个参数都是 this 的指向对象，第二个参数差别就来了：
 - call的参数是直接放进去的，第二第三第n个参数全都用逗号分隔，直接放到后面  obj.myFun.call(db,'成都', ... ,'string' )；
 - apply的所有参数都必须放在一个数组里面传进去  obj.myFun.apply(obj2,['成都', ..., 'string' ]);
 - bind除了返回是函数以外，它的参数和call 一样。
　　　　
　　当然，三者的参数不限定是string类型，允许是各种类型，包括函数 , object 等等！