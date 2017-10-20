---
title: 读《javaScript高级程序设计－第6章》之理解对象
date: 2017-10-18 19:10:13
tags: js
---
ECMA－262把对象定义为：无序属性的集合，其属性可以包含基本值、对象或函数。所以，我们可以理解对象就是名值对的集合，名就是对象的每个属性的名字，而每个名字都映射到一个值。
## 一、创建对象
创建对象有两种方式：
#### 方式一
```
var person=new Object();
person.name=“Jone”;
person.age=20;
person.job=“Software Engineer”;

person.sayName=function(){
    alert(this.name);
};
```
#### 方式二
```
var person={
    name:”Jone”,
    age:20,
    job:“Software Engineer”,
    
    sayName:function(){
        alert(this.name);
    }
};
```
这两种方式创建的对象都是一样的。也可以灵活的混合使用，但要记住`var person=new Object()`和
```
var person={
    name:”Jone”,
    age:20,
    job:“Software Engineer”,
    
    sayName:function(){
        alert(this.name);
    }
}
```
都是在为person赋值，**不可重复赋值，如果重复使用就相当于前面的值放弃，使用后来重新赋的值。或者说都是在给person指向了一个新的地址，地址里存着新的对象。person确定是一个引用类型了，就可以在任意的地方用点来为它添加属性和访问属性，例如：`person.sex=“女”`。person用点访问时不会再为person更改指向地址，更改的是地址里存着的对象。**
## 二、对象属性的特性
对象的属性可以分为两种属性：数据属性，访问器属性。两种类型的属性有各自的特性。

- 数据属性：
```
[[configurable]]:表示能否通过delete删除属性，能否修改属性的特性，或者能否把属性修改为访问器属性。
[[enumerable]]:表示能否通过for-in循环返回属性。
[[writable]]:表示能否修改属性的值。
[[value]]:包含这个属性的数据值。读取属性值的时候，从这个位置读取；写入属性值的时候，把新值保存在这个位置。这个特性的默认值是undefined。
像上面的例子那样直接在对象上定义的属性，它们的configurable、enumerable、writable这些特性默认值为true。
```

- 访问器属性：
```
[[configurable]]:表示能否通过delete删除属性，能否修改属性的特性，或者能否把属性修改为访问器属性。
[[enumerable]]:表示能否通过for-in循环返回属性。
[[get]]:在读取属性时调用的函数。默认值是undefined
[[set]]:在写入属性时调用的函数。默认值是undefined
像上面的例子那样直接在对象上定义的属性，它们的configurable、enumerable这些特性默认值为true。
```
访问器属性的使用方式即：设置一个属性的值会导致其他属性发生变化。
 **访问器属性的`get`、`set`特性不能直接定义,而是使用`Object.defineProperty()`来定义，属性的`get`、`set`特性和`writable`、`value`特性不能同时存在。**

- 特性的访问方法：
1. Object.defineProperty()
例如：
```
var book={};
Object.defineProperty(book,”year”,{
    configurable:true,
    value:2004
});
Object.defineProperty(person,”_year”,{
    configurable:true,
    get:function(){
        return this.year;
    },
    set:function(newValue){
        if(newValue>2004){
            this.year=newValue;
        }
    }
});
```
**创建一个新属性，或修改一个属性的特性。创建一个新属性时，如果不指定，`configurable`、`enumerable`、`writable`默认值都为`false`。`configurable`一旦被设置为`false`，就不能再把它变回`true`了，此时，再调用`Object.defineProperty()`修改除`writable`之外的特性都会报错。**

2. Object.defineProperties()
可以一次性定义多个属性。
```
var book={};
Object.defineProperties(book,{
    year:{
        configurable:true,
        value:2004
    },
    _year:{
        configurable:true,
        get:function(){
            return this.year;
        },
        set:function(newValue){
            if(newValue>2004){
                this.year=newValue;
            }
        }
    }
});
```
3. Object.getOwnPropertyDescriptor()
用来读取属性的特性。接受两个参数：属性所在的对象和要读取其特性的属性名,返回的时其特性的对象
例如：
```
var descriptor=Object.getOwnPropertyDescriptor(book,”year”);
            alert(descriptor.value);//2004
            alert(descriptor.configurable);//true
```
*读《javaScript高级程序设计》这本书的第6章面向对象的程序设计，我做了3篇笔记。这是第一篇，后面还有两篇，分别是封装类和继承。*
*以前一直认为真正理解了一个问题，你就能把它讲清楚，讲清楚了再把它写清楚就容易了，现在发现要写清楚真的太难了，要斟酌每句话都不是废话，没有歧义，尽量用少的字句等等。废话了好久也不知道写清楚了吗。*
*如果哪里有问题欢迎指出。*