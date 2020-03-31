---
layout: pages
title: javascript设计模式
date: 2020-03-07 18:26:17
categories: "JavaScript"
tags: ["JavaScript"]
---

# 面向对象
## 概念
面向对象也即是OOP，Object Oriented Programming，是计算机的一种编程架构，OOP的基本原则是计算机是由子程序作用的单个或者多个对象组合而成，包含属性和方法的对象是类的实例，但是JavaScript ES5中没有类的概念，而是直接使用对象来实现编程;ES6开始则有类的概念。
了解面向对象时，则先了解以下两个概念：
类，即我们定义一个类：
```js
class Person{
    constructor(name){
        this.name = name
    }
    getName(){
        return this.name
    }
}
```
而对象，就是我们可以用这个类创建多个对象:
```js
let p1  = new Person('john')
let p2  = new Person('sun')
```
## 三要素：
### 继承
继承就是将公共方法抽离出来，提高复用，减少冗余；
子类继承父类（extend）；
以上例子为准，我们再创建一个子类
```js
class Student extends Person{
    constructor(name,number){
        super(name);
        this.number = number;
    }
    study(){
        console.log(`${this.name} style`)
    }
}
let p3 = new Student('she','A123');
p3.getname();
p3.study();
```
### 封装
数据的权限和保密（ts有，es5/es6没有此概念）；
`public` 完全开放,默认值；
`protected` 对子类开放
`private` 对自己开放
```js
class Person{
    name    /* 默认publish */
    protected weight   /*  定义protected属性*/
    constructor(name){
        this.name = name;
        this.weight = 88;
    }
    /* 此可以访问 weight*/
}
class Student extends Person{
    number
    private girlfriend
    constructor(name,number){
        super(name)
        this.number = number;
    }
    console.log(this.name) /* √ */
    console.log(this.weight) /* √ */
}
let str = new Student('jhon'
,'A2');
str.girlfriend/* 不能访问 */
str.weight/* 不能访问 */
```
### 多态
同一接口不同实现

## 实例
jQuery就是一个构造函数，面向对象开发
```js
class JQuery(){
    constructor(selector){
        let slice = Array.prototype.slice
        let dom = slice.call(document.querySelectorAll(selector))
        let len = don?dom.length:0
        for(let i=0;i<len;i++){
            this[i] = dom[i]
        }
        this.length = len
        this.selector = selector||''
    }
    html(data){

    }
    addClass(name){

    }
    /* 其他API */    
}
window.$ = function(selector){
    return new JQuery(selector)
}

var $p = $('p');
```
## 为什么要使用面对对象
程序执行：顺序、判断、循环-结构化
面向对象-数据结构化
对于计算机，结构化的才是最简单的
编程应该简单&抽象

# 设计原则
## 何为设计
### 描述
即按照哪一种思路或者标准来实现功能；
功能相同，可以有不同设计方案来实现；
伴随着需求增加，设计的作用才能体现出来；

### 《UNIX/LINUX设计哲学》
准则1：小即是美
准则2：让每个程序只做好一件事
准则3：快速建立原型
准则4：舍弃高频率而取可移植性
准则5：采用纯文本来存储数据
准则6：充分利用软件的杠杆效应（软件复用）
准则7：使用shell脚本来提高杠杆效应和可移植性
准则8：避免强制性的用户界面
准则9：让每个程序都称为过滤器

小准则：允许用户定制环境
小准则：尽量使操作系统内核小而轻量化
小准则：使用小写字母并尽量短写
小准则：沉默是金
小准则：各部分之和大于整体
小准则：寻求90%的解决方案

### SOLID五大设计原则
`S-单一职责原则`
一个程序只做好一件事
如果功能过于复杂就拆分，每个部分保持独立
`O-开放封闭原则`
对修改封闭，对扩展开放；
增加需求时，扩展新代码，而非修改已有的；
这是软件设计的终极目标
`L-李氏置换原则`
子类能覆盖父类
父类能出现的地方子类就能出现
JS中使用较少（弱类型&继承使用较少）
`I-接口独立原则`
保持接口的单一独立，避免出现“胖接口”
JS中没有接口（ts除外），使用较少
类似于单一职责原则，这里更关注接口
`D-依赖导致原则`
面向接口编程，依赖于抽象而不依赖于具体
使用方只关注接口而不关注具体类的实现
JS中使用较少（没有接口，弱类型）

# 设计模式分类
## 创建型
工厂模式（工厂方法模式，抽象工厂模式，建造者模式）
单例模式
原型模式
## 结构型
适配器模式
装饰器模式
代理模式
外观模式
桥接模式
组合模式
享元模式
## 行为型-1
策略模式
模板方法模式
观察者模式
迭代模式
指责连模式
命令模式
## 行为型-2
备忘录模式
状态模式
访问者模式
中介者模式
解释器模式

# 工厂模式
## 介绍
将new 操作单独封装
遇到new时，就要考虑是否该使用工厂模式
```js
class Product{
    constructor(name){
        this.name = name
    }
    init(){
        console.log('init')
    }
    fn1(){
        console.log('fn1')
    }
}
class Creator{
    createProduct(name){
        return new Product(name)
    }
}
let creator = new Creator()
let p = creator.create('p1')
p.init()
p.fun1()
```
## 场景
jQuery - $('div')
React.createElement
vue异步组件
## 设计原则验证
构造函数和创建者分离
符合开放封闭原则
# 单例模式
## 介绍
系统中被唯一使用
一个类只有一个实例
```js
class SingleObject{
    login(){
        console.log(11)
    }
}
SingleObject.getInstance = (function(){
    let instance
    return function(){
        if(!instance){
            instance = new SingleObject()
        }
        return instance
    }
})()
let obj1 = SingleObject.getInstance();
obj1.login()
let obj2 = SingleObject.getInstance();
obj2.login()
obj1===obj2  /* true */
```

## 场景
jQuery 只有一个$
```js
if(window.jQuery!=null){
    return window.JQuery
}else{
    /* 初始化 */
}
```
## 设计原则严重
符合单一职责原则，只实例化唯一的对象
没法具体开放封闭原则，但是绝对不违法开放封闭原则

# 适配器模式
## 介绍
旧接口和使用者不兼容
中间加一个适配转换接口
```js
class Adaptee{
    specificRequest(){
        return '德国标准插头'
    }
}
class Target{
    constructor(){
        this.adaptee = new Adaptee()
    }
    request(){
        let info = this.adaptee.specificRequest()
        return `${info}-转换器-中国标准插头`
    }
}
/* test */
let target = new Target()
let res = target.request()
console.log(res)
```

## 场景
封装旧接口
由于接口改变，对之前的接口进行多一层封装；

vue的conputed（计算）
对data进行一层封装

# 装饰器模式

## 介绍
为对象添加新功能
不改变其原有的结构和功能
```js
class Circle{
    draw(){
        console.log('画画')
    }
}
class Decorator{
    constructor(circle){
        this.circle = circle
    }
    draw(){
        this.circle.draw()
        this.setRedBorder(circle)
    }
    setRedBorder(circle){
        console.log('设置红色边框')
    }
}
// 测试代码
let circle = new Circle()
circle.draw()
let dec = new Decorator(circle)
dec.draw()
```

## 场景
`ES7装饰器`
```js
/* 例子1 */
function minxins(...list){
    return function(target){
        Object.assign(target.prototype,...list)
    }
}
const Foo = {
    foo(){
        console.log('foo')
    }
}
@mixins(Foo)/* ES7语法*/
class MyClass{

}
let obj = new MyClass()
obj.foo()

/* 例子2 */
class log(target,name,descriptor){
    let oldValue = descriptor.value
    descriptor.value = function(){
        console.log('新增装饰器')
        return oldValue.apply(this,arguments)
    }
    return descriptor 
}
class Math{
    @log
    add(a,b){
        return a+b
    }
}
let math = new Math()
const result = math.add(2+1)
/* 打印则会打印出封装过的装饰器内容 */
console.log(result)
```
`core-decorators`
第三方开源lib
提供常用的装饰器
```js
import { readonly } from ' core-decorators '
class Person{
    @readonly   /* 不可修改 */
    name(){
        return 'shealain'
    }
}
let p = new Person()
alert(p.name())
p.name = function(){}/* 报错 */
```
## 设计原则验证
将现有对象和装饰器进行分离，两者独立存在
符合开放封闭原则

# 代理模式

## 介绍
使用者无权访问目标对象
中间加代理，通过代理做授权和控制

```js
class ReadImg{
    constructor(fileName){
        this.fileName = fileName
        this.loadFromDisk()
    }
    display(){
        console.log('display...' + this.fileName)
    }
    loadFromDisk(){
        console.log('loading...' + this.fileName)
    }
}
class ProxyImg{
    constructor(fileName){
        this.realImg = new ReadImg(fileName)
    }
    display(){
        this.realImg.display()
    }
}
let proxyImg = new ProxyImg('banner.png')
proxyImg.display()
```

## 场景
`网页事件代理`
```css
<ul id="ul">
    <li>1</li>
    <li>2</li>
</ul>
```
```js
var ul = document.getElementById('ul')
ul.addEventListener('click',function(e){
    var target = e.target
    if(e.target.nodeName==='li'){
        /* 冒泡原理 */
        console.log(target.innerHTML)
    }
})
```
`jQuery $.proxy`
```js
$('#ul').click(function(){
    /* 把this代理进去，使里外的this指向同一域 */
    var fn = $.proxy(function(){
        $(this).css('background','red')
    },this)    
    setTimeout(fn,100)
})

```
`ES6 Proxy`
```js
/* 明星 */
let star = {
    name:'she',
    age:25,
    phone:'15323236023'
}
/* 经纪人 */
let agent = new Proxy(star,{
    get:function(target,key){
        if(key==='phone'){
            /* 返回经纪人电话 */
            return '135667766555'
        }
        if(key==='price'){
            /* 明星报价 */
        }
        return target[key]
    },
    set:function(target,key,val){
        if(key==='customPrice'){
            if(val<100000){
                throw new Error('价格太低')
            }else{
                target[key] = val
                return true
            }
        }
    }
})
/* 测试 */
console.log(agent.name)
console.log(agent.age)
console.log(agent.phone)
console.log(agent.price)
agent.customPrice = 80000/* 报错，价格太低 */
```
## 设计原则验证
代理类和目标类分离，隔离开目标类和使用者
符合开放封闭原则
## 模式比较
代理模式 vs 适配器模式
适配器模式：提供一个不同的接口（如不同版本的接口）
代理模式：提供一模一样的接口
代理模式vs装饰器模式
装饰器模式：扩展功能，原有功能不变且可直接使用
代理模式：显示原有功能，但是经过限制或者阉割之后的

# 外观模式

## 介绍
为子系统中的一组接口提供了一个高层接口
使用者使用这个高层接口

## 场景
```js
function(elem,type,selector,fn){
    if(fn==null){
        fn = selector
        selector = null
    }
}
/* 调用 */
bindEvent(elem,'click','#div1',fn)
bindEvent(elem,'click',fn)
```
## 设计原则验证
不符合单一职责原则和开放封闭原则，因此谨慎使用，不可滥用
# 观察者模式
## 介绍
发布 & 订阅
一对多
```js
/* 主题，保存状态，状态变化之后触发所有观察者对象 */
class Subject{
    constructor(){
        this.state = 0
        this.objservers = []
    }
    getState(){
        return this.state
    }
    setState(state){
        this.state = state
        this.notifyAllObservers()
    }
    notifyAllObservers(){
        this.objservers.forEach(observer=>{
            observer.update()
        })
    }
    attach(observer){
        this.observer.push(observer)
    }
}
/* 观察者 */
class Observer{
    constructor(name,subject){
        this.name = name
        this.subject = subject
        this.subject.attach(this)
    }
    update(){
        console.log(this.name + 'update')
    }
}
/* 测试 */
let s= new Subject()
let o1 = new Observer('o1',s)
let o2 = new Observer('o2',s)
let o3 = new Observer('o3',s)
s.setStage(1)
```
## 场景
网页事件绑定
```js
<button id="btn1">btn</button>
$('btn1').click(function(){
    console.log(1)
})
```
Promise
```js
var promise = new promise(function(resolve,reject){
    setTimeout(function(){
        resolve('success')
    },100)
})
return promise
```
jQuery callbacks
```js
/* 自定义事件 */
var callbacks = $.Callbacks()
/* 观察者 */
callbacks.add(function(info){
    console.log('fn1',info)
})
callbacks.add(function(info){
    console.log('fn2',info)
})
callbacks.add(function(info){
    console.log('fn3',info)
})
/* test */
callbacks.fire('第一次触发')
callbacks.fire('第二次触发')
```
nodejs 自定义事件
```js
const EventEmitter = require('events').EventEmitter
/* 例子1 */
const emitter1 = new EventEmitter()
/* 监听some事件 */
emitter1.on('some',info=>{
    console.log('fn1',info)
})
/* 监听some事件 */
emitter1.on('some',info=>{
    console.log('fn2',info)
})
/* 触发some事件 */
emitter1.emit('go')
/* 例子2 - 继承*/
class Dog extends EventEmitter{
    constructor(name){
        super()
        this.name = name
    }
}
let sim = new Dog('sim')
sim.on('bark',function(){
    console.log(tjos.name,'barked-1')
})
sim.on('bark',function(){
    console.log(tjos.name,'barked-2')
})
sim.emit('bark')
```
## 其他场景
nodejs中：处理http请求；多进程通讯
vue和React组件生命周期触发
vue Watch
## 设计原则验证
主题和观察者分离，不是主动触发而是被动监听，两者解耦
符合开放封闭原则

# 迭代器模式
## 介绍
顺序访问一个集合（有序列表）
使用者无需知道集合的内部结构（封装）
## 示例
```js
var arr = [1,2,3]
var nodeList = document.getElementsByTagName('a')
var $a = $('a')

/* 遍历数组 */
arr.forEach(function(item){
    console.log(item)
})
/* 遍历nodeList */
var i,length = nodeList.length
for(i=0;i<length;i++){
    console.log(nodeList[i])
}
/* 遍历$a */
$a.each(function(key,elem){
    console.log(key,elem)
})
/* 写一个统一方法，能对三个不同对象进行遍历 */
 function each(data){
     var $data = $(data)/*使用迭代器  */
     $data.each(function(key,val){
         console.log(key,val)
     })
 }
 each(arr)
 each(nodeList)
 each($a)

```
## 迭代器模式
```js
/* 迭代器 */
class getIterator{
    constructor(container){
        this.list = container.list
        this.index = 0
    }
    next(){
        if(this.hasNext()){
            return this.list[this.index++]
        }
        return null
    }
    hasNext(){
        if(this.index>=this.list.length){
            return false
        }
        return true
    }
}
class Container{
    constructor(list){
        this.list = list
    }
    /* 生成遍历器 */
    getIterator(){
        return new this.getIterator(this)
    }
}
/* test */
let arr = [1,2,3,4,5]
let container = new Container(arr)
let iterator = container.getIterator()
while(iterator.hasNext()){
    console.log(iterator.next())
}
```
## ES6Iterator
`为何存在？`
ES6语法中，有序集合的数据类型已经有很多
Array，Map，Set，String，TypedArray,arguments,NodeList
需要有一个统一的遍历接口来遍历所有数据类型
`ES6Iterator 是什么`
以上数据类型，都有[Symbol.iterator]属性
属性值是函数，执行函数返回一个迭代器
这个迭代器就有next方法可顺序迭代子元素
可运行Array.prototype[Symbol.iterator]来测试
```js
/* 例子1 */
function each(data){
    /* 生成遍历器 */
    let iterator = data[Symbol.iterator]()
    let item = {done:false}
    while(!item.done){
        item = iterator.next()
        if(!item.done){
            console.log(item.value)
        }
    }
}
/* 例子2 */
function each(data){
    /* 带有遍历器特性的对象：data[Symbol.iterator] 有值*/
    for(let item of data){
        console.log(item)
    }
}
/* test */
var arr = [1,2,3]
var nodeList = document.getElementsByTagName('a')
var $a = $('a')
each(arr)
each(nodeList)
each($a)
```
## 设计原则验证
迭代器对象和目标对象分离
迭代器将使用者与目标对象隔离开
符合开放封闭原则

# 状态模式
## 介绍
一个对象有状态变化
每次状态变化都会触发一个逻辑
不能总是用if...else 来控制
```js
/* 状态 */
class State{
    constructor(color){
        this.color = color
    }
    handle(context){
        console.log('turn to' + this.color)
        context.setState(this)
    }
}
/* 主体 */
class Context{
    constructor(){
        this.state = null
    }
    /* 获取状态 */
    getState(){
        return this.state
    }
    /* 设置状态 */
    setState(state){
        this.state = state
    }
}
/* test */
let context=  new Context()
let green = new State('green')
let yellow = new State('yellow')
let red = new State('red')

green.handle(context)
console.log(context.getState)

```
## 场景
`有限状态机`
有限个状态、以及在这些状态之间的变化
如交通信号灯
使用开源lib:javascript-state-machine
地址：github.com/jakesgordon/javascript-state-machine
<!-- 例子，收藏和取消 -->
```js
import StateMachine from 'javascript-state-machine'
/* 初始化状态机模式 */
let fsm = new StateMachine({
    init:'收藏',
    transitions:[{
        name:'doStore',
        from:'收藏',
        to:'取消收藏'
    },{
        name:'deleteStore',
        from:'取消收藏',
        to:'收藏'
    }],
    methods:{
        /* 监听执行收藏 */
        onDostore:function(){
            console.log('收藏成功！')
            updateText()
        },
        /* 监听执行收藏 */
        onDeleteStore:function(){
            console.log('已取消收藏！')
            updateText()
        }
    }
})
let btn =$('#btn')
$('#btn').on('click',function(){
    if(fsm.is('收藏')){
        fsm.doStore()
    }else{
        fsm.deleteStore()
    }
})

/* 更新按钮文案 */
function updateText(){
    $('#btn').text(fsm.state)
}
/* 初始化状态 */
updateText()
```
`写一个简单的Promise`
```js
import StateMachine from 'javascript-state-machine'

/* 初始化状态机模式 */
let fsm = new StateMachine({
    init:'pending',/* 初始化状态 */
    transitions:[{
        name:'resolve',
        from:'pending',
        to:'fullfilled'
    },{
        name:'reject',
        from:'pending',
        to:'rejected'
    }],
    methods:{
        /* 监听resolve */
        onResolve:function(state,data){
            /* state-当前状态机实例；data-fsm.resolve传递的参数*/
            data.successList.forEach(fn=>fn())
        },
        /* 监听reject */
        onReject:function(){
            data.failList.forEach(fn=>fn())
            /* state-当前状态机实例；data-fsm.resolve传递的参数 */
        }
    }
})

/* 定义Promise */
class MyPromise{
    constructor(fn){
        this.successList = []
        this.failList = []

        fn(function(){
           /*  resolve函数 */
           fsm.resolve(this)
        },function(){
            /* reject函数 */
            fsm.reject(this)
        })
    }
    then(successFn,failFn){
        this.successList.push(successFn)
        this.failList.push(failFn)
    }
}

/* 测试代码 */
function loadImg(src){
    function fn(resolve,reject){
        let img = document.createElement('img')
        img.onload = function(){
            resolve(img)
        }
        img.onerror = function(){
            reject()
        }
        img.src = src
    }
    const promise = new Promise(fn)
    return promise
}
let src = '../img'
let result = loadImg(src)
result.then(function(){
    console.log('ok')
},function(){
    console.log('fail')
})
```
## 设计原则验证
将状态对象和主题对象分离，状态的变化逻辑单独处理
符合开放封闭原则

# 其他设计模式
`优先级划分依据`
1.不常用
2.对应不到经典的应用场景
## 原型模式
### 概念
clone自己，生成一个新对象
java默认有clone接口，不用自己实现

`js中的应用-Object.create`
```js
/* 一个原型对象 */
let prototype = {
    getName:function(){
        return this.first + '' + this.last
    }
}
/* 基于原型创建x */
let x=Object.create(prototype)
x.first = 'A'
x.last = 'B'
alert(x.getName())
/* 基于原型创建y */
let y=Object.create(prototype)
y.first = 'C'
y.last = 'D'
alert(y.getName())
```
对比JS中的原型prototype
prototype可以理解为ES6 class的一种底层原理
而class是实现面向对象的基础，并不是服务于某个设计模式
若干年后ES6全民普及，大家可能会忽略掉prototype
但是Object.create却会长久存在
## 桥接模式
### 介绍
用于把抽象化与实现话解耦
使得二者可以独立变化
未找到JS中的经典应用
```js
/* 两者分离独立开来 */
class color{
    
}
class type{

}
```
### 设计原则验证
抽象和实现分离，解耦
符合开放封闭原则

## 组合模式
### 概念
生成树形结构，表示“整体-部分”关系
让整体和部分都具有一致的操作方式
### 演示
js经典应用中，未找到这么复杂的数据类型
虚拟DOM中的vnode是这种形式，但是数据类型简单
用js实现一个菜单，不算经典应用，与业务相关

原则
整体和单个节点的操作是一致的
整体和单个节点的数据结构也保持一致
### 设计原则验证
将整体和单个节点的操作抽象出来
符合开放封闭原则

## 享元模式
### 概念
共享内存（主要考虑内存，而非效率）
相同的数据，共享使用
js中未找到经典应用场景
### 示例
`网页事件代理`（代理模式，事件代理）
```css
<ul id="ul">
    <li>1</li>
    <li>2</li>
</ul>
```
```js
var ul = document.getElementById('ul')
ul.addEventListener('click',function(e){
    var target = e.target
    if(e.target.nodeName==='li'){
        /* 冒泡原理 */
        console.log(target.innerHTML)
    }
})
```
### 设计原则验证
将相同的部分抽象出来
符合开放封闭原则
## 策略模式
### 概念
不同策略分开处理
避免大量出现if...else或者switch...case
js中未找到经典应用场景
### 演示
```js
/* 
相同代码用父类进行；
if else 用不同类进行处理，继承父类
 */
```
## 模板方法模式
业务场景常用，多个方法对外包装成一个
```js
    class Action{
        handle(){
            handle1()
            handle2()
            handle3()
        }
        handle1(){}
        handle2(){}
        handle3(){}
    }
```
## 指责连模式
### 概念
一步操作可能分位多个职责角色来完成
把这些角色都分开，然后用一个链串起来
将发起者和各个处理者进行隔离

### 演示
```js
class Action{
    constructor(name){
        this.name = name
        this.nextAction = null
    }
    setNextAction(action){
        this.nextAction = action
    }
    handle(){
        console.log(`${this.name}审批`)
        if(this.nextAction!=null){
            this.nextAction.handle()
        }
    }
}
/* 测试代码 */
let a1 = new Action('组长')
let a2 = new Action('经理')
let a3 = new Action('总监')
a1.setNextAction(a2)
a2.setNextAction(a3)
a1.handle()
```
`js中的链式操作`
职责链模式和业务结合较多，js中能联想到链式操作
jQuery的链式操作，Promise.then的链式操作
### 设计原则验证
发起者于各个处理进行隔离
符合开放封闭原则

## 命令模式
### 概念
执行命令时，发布者和执行者分开
中间加入命令对象，作为中转站
```js
/* 接收者 */
class Receiver{
    exec(){
        console.log('执行')
    }
}
/* 命令者 */
class command{
    constructor(receiver){
        this.receiver = receiver
    }
    cmd(){
        console.log('执行命令')
        this.receiver.exec()
    }
}
/* 触发者 */
class Invoker{
    constructor(command){
        this.command = command
    }
    invoke(){
        console.log('开始')
        this.command.cmd()
    }
}

/* test */
/* 士兵 */
let  soldier = new Receiver()
/* 小号手 */
let trumpeter = new Comment(soldier)
/* 将军 */
let general = new Invoker(trumpeter)
general.invoke()
```
### 设计原则验证
命令对象于执行对象分开，解耦
符合开放封闭原则

## 备忘录模式
### 概念
随时记录一个对象的状态变化
随时可以恢复之前的某个状态（如撤销功能）
未找到js中经典应用，除了一些工具（编辑器）

```js
/* 备忘类 */
class Memento{
    constructor(content){
        this.content = content
    }
    getContent(){
        return this.content
    }
}
/* 备忘列表 */
class CareTaker{
    constructor(){
        this.list = []
    }
    add(memento){
        this.list.push(memento)
    }
    get(index){
        return this.list[index]
    }
}
/* 编辑器 */
class Editor{
    constructor(){
        this.content = null
    }
    setContent(content){
        this.content = content
    }
    getContent(){
        return this.content
    }
    saveContentToMemento(){
        return new Memento(this.content)
    }
    getContentFromMemento(memento){
        this.content = memento.getContent()
    }
}

/* 测试代码 */
let editor = new Editor()
let careTaker = new CareTaker()

editor.setContent('111')
editor.setContent('222')

careTaker.add(editor.saveContentToMemento())/* 将当期内容备份 */
editor.setContent('333')
careTaker.add(editor.saveContentToMemento())/* 将当期内容备份 */
editor.setContent('444')

console.log(editor.getContent())
editor.getContentFromMemento(careTaker.get(1))
console.log(editor.getContent())

```

### 设计原则验证
状态对象于使用者分开，解耦
符合开放封闭原则

## 中介者模式
```js
class A{
    constructor(number){
        this.number = number
    }
}
class B{
    constructor(number){
        this.number = number
    }
}
class Mediator{
    constructor(a,b){

    }
}
/* test */
let a = new A(1)
let B = new B(1)
let m = new Mediator(a,b)
```
## 访问者模式
将数据操作和数据结构进行分离
使用场景不多

## 解释器模式
描述语言语言如何定义，如何解释和编译
用于专业场景

# 关于面试
能说出课程重点讲解的设计模式即可








