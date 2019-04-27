# HTML

### HTML4.01

### XHTML1.0

### HTML5

###标签兼容插件

# CSS

### CSS2

### CSS3

###渐进式设计

###兼容问题

# JAVSCRIPT



### js基础

#####变量

##### 数据类型

基础数据类型  

```
undefined
null
Number
Boolean
String
```



引用数据类型

```
数组


对象


对象的深拷贝和浅拷贝

基本类型的包装类型( Boolean()  String() Number())
```

### 运算

##### 数学运算

##### 逻辑运算

### 流程控制

##### 分支流程控制  

```
if(){}
else if(){}
...
else{
    
}

switch(){
    case value:
    	break;
    ...
    default:
    	
}
```

##### 循环

```
for(var i=0;i<=199;i++){
    
}
while(){
    
}
do{}while();

```



### 函数

```
定义函数

匿名函数

匿名函数作为参数 和 返回值
立即执行匿名函数
函数递归
作用域:
function heloo(){
    this=window
    arguments数组
}
hello.apply(window,[10,20,30]);
apply改变当前函数内部对象作用域

闭包：
function sayHello(){
    document.getElement
}

```

### 对象

```创建对象的方式
Object类型:
var o=new Object();
var o={}; 字面量定义类型
创建对象的方式:
1.工厂模式
function objectFactory(name,age,job){
    var o=new Object();
    	o.name=name;
    	o.age=age;
    	o.job=job;
    	o.sayHello=function(){
            
    	}
    	return o;
}
var obj=objectFactory(100,100,100);
2.构造函数 可以用来检测对象的类型
function Person(name,age,jon){
    this.name=name;
    this.age=age;
    this.job=job;
    this.sayHello=function(){
        
    }
}
var p1=new Person();
p1.constructor==>指向Person;
console.log(p1 instanceof Person); true
console.log(p1 instanceof Object); true  继承自Object
构造可以当做普通函数 内部的this 指向当前作用域对象 一般是window Global
sayHello是每个对象会为其创建一个函数对象:
function sayHello(){
    
}
function Person(name,age,job,sayHello){
    this.name=name;
    this.age=age;
    this.job=job;
    this.sayHello=sayHello; 共用一个外部的全局函数
}
3.原型模式
prototype属性是一个指针 指向一个对象.这个对象包含特性类型的所有共享属性和方法;
通过构造函数创建的对象实例的原型对象;
function Person(){
    
}
Person.prototype.name="";
Person.prototype.age=20;
Person.prototype.job="工作";
Person.prototype.sayHello=function(){
    
}
//Person.prototype 指向Person的原型对象, 原型对象的constructor属性指针指向Person函数
var p1=new Person();//p1对象 相当于继承自了  Person的prototype原型对象 p1.__proto__指向原型对象
var p2=new Person)();//p1对象 相当于继承自了  Person的prototype原型对象
//更为简单的模式  ,  切断了原原型对象所有信息 包含constructor 现在不会指向 Person.
Person.prototype={
    name:'',
    age:'',
    job:'',
    sayHello:function(){
        
    }
}; 
//原型对象的问题 原型的属性如果为引用类型，那么依然会共享整个属性
Person.prototype.subject=['11','22','333'];
4.组合使用构造函数模式和原型模式
function Person(name,age,job){
    this.name=name;
    this.age=age;
    this.job=job;
    this.friend=[11,22,33];
}
Person.prototype={
    constructor:Person,
    sayHello:function(){
        this.name;
    }
};
p1=new Person();// friend不会共享
p2=new Person();// friend不会共享
5.稳妥方式
function Person(){
    var o=new Object();
    var username=username;
    var age=20;
    o.sayHello=function(){
        
    }
    return o;
}
```

```
继承:
原型链:
function FatherType(){
    this.subjects=[11,22,33];
}
function SonType(){
    
}
Sontype.prototype=new FatherType();// 实现了继承

var p1=new SonType();  //subjects是引用类型 p1和p2共用
var p2=new SonType();  //
构造函数继承:
function FatherType(){
    this.subjects=[11,22,33];
}
function SonType(){
    FatherType.apply(this,arguments);
}
var p1=new SonType();
var p2=new SonType();
组合继承:
function FatherType(){
    this.subjects=[11,22,33];
}
function SonType(){
    FatherType.apply(this,arguments);
}
SonType.prototype=new FathType();
SonType.proptotype.constructor=SonType;
Sontype.prototype.sayAge=function(){
    
}
var p1=new SonType();
var p2=new SonType();

```



### DOM和BOM对象模型

```
NodeList

事件


```



​																																														

