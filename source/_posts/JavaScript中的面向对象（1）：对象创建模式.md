---
title: JavaScript中的面向对象（1）：对象创建模式
tags: []
number: 2
date: 2017-03-27 05:18:01
---

# 对象

JS中的对象是无序属性的集合，属性可以包括基本值、对象、函数。简而言之，JS中的对象就是一组键值对。

# 创建对象

## 工厂模式

工厂模式是用函数将创建对象的细节封装起来。

```
function createPerson(name){

var o = new Object();
o.name = name;
return o;

}

```

特点：显式地创建对象，有return
问题：无法解决对象识别的问题

## 构造函数模式

类似Object、Array等原生构造函数，我们可以自定义构造函数。

```
function Person(name){
this.name = name;
this.sayHello = function(){
alert('hello' + this.name)}
}

var person1 = new Person("Peter");
var person2 = new Person("Mike");
```

特点：不显式地创建对象，没有return，构造函数的首字母大写，不同实例之间具有相同的constructor属性。
问题：不同实例之间的同名函数不相等（具有不同的作用域链和标识符解析）
解决：将函数的定义移到构造函数外部。


```
function Person(name){
this.name = name;
this.sayHello = sayHelo;
}

function sayHello(){
alert('hello' + this.name)}
}

```

问题：sayHello定义在全局作用域，但实际上只能被某个对象调用。名不副实。2. 在需要定义很多方法的情况下，需要定义很多全局函数，违背封装的理念。
解决：原型模式

## 原型模式

每一个函数都有一个原型属性，这个原型是一个指针，指向一个对象。
这个对象包含同一构造函数所创建的所有实例所共享的属性和方法。

```
function Person(){
}

Person.prototype.name = 'Mike';
Person.prototype.sayHello = function(){
alert('hello'+this.name);
}

```

事实上，上文提到的constrcutor属性，也存在于原型对象中。
访问对象属性时，首先查找实例本身，然后查找原型对象。如果实例本身具有该属性，就会屏蔽原型对象中的同名属性。

用对象字面量来重写

```
function Person(){
}

Person.prototype = {
name:'Mike';
sayHello = function(){
alert('hello'+this.name);
}

```
此时

```
var mike = new Person
mike.constructor == Person //false
mike.constructor == Object //false

```

更正：

```
Person.prototype = {
constructor:Person
name:'Mike';
sayHello = function(){
alert('hello'+this.name);
}
```

进一步更正：

```
Object.defineProperty(Person.prototype,"constructor",{
enumerable: false,
value:Person
})
```

## 构造函数与原型模式组合

```
function Person(name){
this.name = name;
this.friends = ['a','b']}

Person.prototype = {
constructor:Person;
sayHello: function(){
alert('hello'+this.name)
}
}
```

优点：每个实例拥有自己的属性，不会互相干扰。

## 动态原型模式

```
function Person(name){
this.name = name;
this.friends = ['a','b']}

if(typeof sayHello != function){ // 只需判断一个
Person.prototyp.sayHello = function(){
alert('hello'+this.name)
}
Person.prototyp.sayBye = function(){
alert('Bye'+this.name)
}
}
```

优点：将所有信息封装在构造函数中，而只在第一次初始化时，添加原型方法。

## 寄生构造函数模式

在不改变某对象原型的情况下，添加新的方法。

```
function SpecialArray(){

var values = new Array();

values.toPipedString = function(){
return this.join('|');
}

return values;

}
```

缺点：对象与构造函数之间没有关系，不能使用instanof操作符。

## 稳妥构造函数模式

```
function Person(name){
var o = new Object();
o.sayName = function(){
alert(name)
}
return o;
}

var mike = Person('mike');
```

特点：不使用new操作符，实例方法中不引入this。
缺点：对象与构造函数之间没有关系，不能使用instanof操作符。
