---
title: JS
description: 
published: true
date: 2024-08-06T08:03:57.130Z
tags: 
editor: markdown
dateCreated: 2024-08-06T08:03:57.130Z
---

[现代 JavaScript 教程](https://zh.javascript.info/)
# ES6
## 1 let、const
var声明变量存在的问题
### var
**var 会造成变量提升**
```javascript
console.log(a);
var a = 10;		//output: undefined (undefind:声明变量但未赋值)
```
因为使用var生命变量的时候, var a 会被提前声明,编辑器会将其变成如下执行
```javascript
var a;
console.log(a);
var a = 10;
```
**var能对一个变量进行多次声明**，后面声明的变量会覆盖前面声明的变量
```javascript
var a = 10;
console.log(a);	// 10
var a = 30;
console.log(a); // 30
```
**在函数内部使用声明时为局部变量，而如果在函数内部不使用var 声明，则为全局变量**
```javascript
var a = 30;

function test(){
  var a = 10
}
test()
console.log(a)  // 30
---------------------
var a = 30;
function test2(){
  a = 10;
}
test2()
console.log(a)  // 10
```
### let
**没有变量提升**
```javascript
console.log(a)  // Uncaught ReferenceError: Cannot access 'a' before initialization
let a = 10
```
**是一个块级作用域**
```javascript
console.log(b) //ReferenceError: 'b' is no defined
if(1==1){
  let b = 10
}
```
**不能重复声明**
```javascript
let a = 1;
let a = 3;
console.log(a); // 'a' has already been declared
```
### const
**用于声明常量，一但声明无法修改，块级作用域，没有变量提升**
```javascript
const person = {
  name:'Mike'
}
preson.name='Amy'
console.log(person)
```
可以修改常量对象内部的属性
## 2 模板字符串
```html
<div class="test">
  <ul>
    <li></li>
  </ul>
</div>
<script>
  let id =1;
  let username = 'Mike'
  const div = document.querySelector('.test')
  div.innerHTML=`
    <ul>
    <li id='${id}'>${username}</li>
  	</ul>
  `
</script>
```
 
## 3 函数默认值
es5 中给函数设置默认值
```javascript
function test(){
  a = a || 10;
  b = b || 20；
  retrun a+b;
}
add()
```
es6写法
```javascript
function test(a = 10;b = 20){ // a的默认值为10，b的默认值为20
  return a+b;
}
console.log(add()) // 30
console.log(add(30)) // 50
```
默认的表达式也可以是一个函数
```javascript
function add(a,b=getVal(5)){
  return a+b;
}
function getVal(val){
  return val+5;
}
add(10)		// 20
```
## 4 函数剩余参数
es5
```javascript
function pick(obj){
  let result = Object.create(null);
  for (let i = 1;i<arguments.length;i++){
    result[arguments[i]] = obj[arguments[i]]
  }
  return result;
}
let book = {
  title:'es6教程',
  autho:'Mike',
  year:2022
}
let bookData = pick(book,'title','year','author')
console.log(bookData);
```
es6 剩余参数：由`...`和一个进跟着的具名参数指定`...keys`(只有函数的最后一个命名参数并添加上...才能作为剩余参数)
```javascript
function pick(obj,...keys){
  let result = Object.create(null);
  for  
}
```
## 扩展运算符
`...`可以将数组表达式，字符串进行展开
```javascript
const arr = [10,20,30,40]
console.log(...arr) //10 20 30 40
const string = 'Hello World!'
console.log(...string) //H e l l o   W o r l d !
```
合并数组
```javascript
test1 = [10,20,30]
test2 = [40,50,60]
test3 = [...test1,...test2]
console.log(test3) [10,20,30,40,50,60]
```
伪数组转化为真数组
```javascript
function add(){
  let arr = Array.from(arguments)
  return arr
}
add(1,2,3)  // [1, 2, 3]	
```
## 5 数组的解构
es5
```javascript
const arr =[100,200,300]
const foo = arr[0]
const bar = arr[1]
const tar = arr[2]
```
es6
```javascript
const arr = [100,200,300]
const [foo,bar,tar] = arr
// [foo,bar,tar] = [100,200,300]
```

获取其中某个位置的成员
```javascript
// 只获取tar的值
const arr = [100,200,300]
const [,,tar] = arr		// 不需要的成员直接用 , 替代
console.log(tar)  // 300
```

获取所有成员的简写方法(返回的是一个数组)
```javascript
const arr = [100,200,300]
const [...tar] = arr
console.log(rest)  //[100,200,300]
```
```javascript
const arr = [100,200,300]
const [,...tar] = arr
console.log(rest)  //[200,300]
```

当解构个数小于被解构的数组长度时,就会按照从前到后的顺序去解构
```javascript
const arr =[100,200,300]
const [acc] = arr
console.log(acc)  //100
```
当解构个数大于数组的长度时,会返回undefined
```javascript
const arr =[100,200,300]
const [,,,acc] = arr
console.log(acc)  //undefined
```

结构数组的时候支持设置默认值
```javascript
const arr = [100, 200, 300]
const [,,ccc=123,aaa=456] = arr
console.log(ccc,aaa)  //300 456
```
示例
```javascript
const path = '/foo/bar/baz'
// es5 写法
const temp = path.split('/')
const rootdir = path.split('/')
console.log(rootdir[1])  // foo

// es6写法
const [,rootdir2] = path.split('/')
console.log(rootdir2)
```

## 6 对象的解构
提取指定成员的值
```javascript
const obj = {name:'zxc',age:'18'}
const {name} = obj
console.log(name)  // zxc
```
重命名成员名 	解构的变量名用来匹配被解构的对象的变量名
```javascript
const obj = {name:'zxc',age:'18'}
const name = 'tom'
const {name: objName} =obj
conosole.log(objName)
```
## 7 箭头函数
```javascript
// es5
function inc(number){
  return  number + i
}

// es6 
const inc = (nummber) =>{
  console.log('test')
  retrun n +1
}
```
案例
```javascript
arr = [1,2,3,4,5]
arr.filter(
  function(item){
    retrun item %2
  })

arr.filter(i => i%2)
```
当箭头函数的返回值只有一个数时，可以省略 return<br />箭头函数没有自己的this

# 其他
## 数组方法
### 改变原数组
> 方法在对arr进行操作后，arr的内容会发生变化（即arr为操作后的结果）

添加方法，返回值为arr的长度<br />删除方法，返回值为删除的那个数
#### push
作用：向数组尾部追加数据,并返回新数组的长度<br />参数：需要添加的数据<br />返回值：进行插入操作后，arr的长度
```javascript
arr = [10,20,30]
const arr1 = arr.push(40) 
console.log(arr1) // 4 ✨数组长度
console.log(arr) // [10,20,30,40]
```
#### pop
作用：删除数组尾部的数据，并返回该数据<br />返回值：删除的数
```javascript
arr = [10,20,30]
const arr1 = arr.pop()
console.log(arr1)  // 30
console.lolg(arr)  //[10,20,30]
```
#### unshift
作用：在数组头部插入数据，并返回新数组长度<br />参数：需要添加的数据<br />返回值：进行操作后，arr的总长度
```javascript
arr = [10,20,30]
const res = arr.unshift(20)
console.log(arr) // [20,10,20,30]
console.log(res) // 4
```
#### shift
作用：删除数组头部数据<br />返回值：删除的数
```javascript
arr = [10,20,30]
arr.shift()
console.log(arr) // [20,30] 
```
#### reverse
作用：反转数组<br />`arr`和返回值均为反转后的结果
```javascript
arr = [10,20,30]
arr.reverse()
console.log(arr)  //[30,20,10]
```
#### sort
作用：对数组中的数据进行排序
```javascript
const arr = [60, 50, 40, 30, 20]
// 默认小到大排序
arr.sort()
console.log(arr) //[20, 30, 40, 50, 60]
```

- arr.sort(function (a,b) {return a-b}) 正排序
- arr.sort(function (a,b) {return b-a}) 倒排序 
#### splice
作用1 截取数据：用来截取数组中的指定部分 下标从0开始
```javascript
const arr = [60, 50, 40, 30, 20]
const res = arr.splice(1,2)
console.log(res) // [50,40]
```
作用2 插入数据：用来将数据插入到数组中的指定位置
```javascript
const arr = [10,20,30]
const res = arr.splice(2,1,40)
```
### 不改变原数组

#### includes
 用来判断一个数组是否包含指定的值，如果是返回 true，否则false。
```javascript
let site = ['runoob', 'google', 'taobao'];
site.includes('runoob'); 
```
### 防抖与节流
防抖：操作时不执行，不操作后才执行<br />节流：到时间必须执行一次
### 对象
对象字面量
```javascript
let user = {
  name:"San",
  age:18
}
```
### 面向对象
类（Class） 类是创建对象的蓝图。在JavaScript中，类通过class关键字来定义。
```javascript
class Person {
  constructor(name, age) {
    // 实例成员
    this.name = name;
    this.age = age;
  }
  // 类成员
  greet() {
    console.log(`Hello, my name is ${this.name} and I am${this.age} years old.`);
  }
}
const person = new Person('Alice', 30);
person.greet(); // 输出： Hello, my name is Alice and I am 30 years old.
```
实例（Instance） 实例是根据类创建的对象。在JavaScript中，使用new关键字和类的构造函数来创建实例。
```javascript
const person1 = new Person('Bob', 25);
const person2 = new Person('Carol', 35);
```
继承（Inheritance） 继承是允许一个类继承另一个类的属性和方法。在JavaScript中，子类可以使用extends关键字来继承父类。
```javascript
class Student extends Person {
  constructor(name, age, grade) {
    super(name, age); // 调用父类的constructor
    this.grade = grade;
  }
  introduce() {
    console.log(`My name is ${this.name} and I am in grade${this.grade}.`);
  }
}
const student = new Student('Eve', 16, '10th');
student.greet(); // 输出： Hello, my name is Eve and I am 16 years old.
student.introduce(); // 输出： My name is Eve and I am in grade 10th.
```
封装（Encapsulation） 封装是指将数据和与数据相关的操作打包在一起，隐藏对象的内部细节。在JavaScript中，可以通过定义私有变量和公共方法来实现封装。
```javascript
class Counter {
  #count = 0; // 私有变量
  increment() {
    this.#count += 1; // 私有方法
  }
  getCount() {
    return this.#count; // 公共方法
  }
}
const counter = new Counter();
counter.increment();
console.log(counter.getCount()); // 输出： 1
```
多态（Polymorphism） 多态是指对象可以以多种形式存在。在JavaScript中，可以通过函数重写（即子类覆盖父类的函数）来实现多态。
```javascript
class Dog {
  bark() {
    console.log('Woof!');
  }
}
class GoldenRetriever extends Dog {
  bark() {
    console.log('Woof woof!');
  }
}
class Poodle extends Dog {
  bark() {
    console.log('Woof woof woof!');
  }
}
const animals = [new Dog(), new GoldenRetriever(), new Poodle()];
animals.forEach(animal => animal.bark());
```
输出：<br />Woof!<br />Woof woof!<br />Woof woof woof!<br />原型（Prototype） 原型是对象的一个属性，它是一个指向另一个对象的引用。在JavaScript中，所有的对象都是通过原型链来共享方法和属性的。
```javascript
function Animal(name) {
  this.name = name;
}
Animal.prototype.speak = function() {
  console.log(`${this.name} makes a noise.`);
};
const cat = new Animal('Tom');
cat.speak(); // 输出： Tom makes a noise.
```
这些是OOP的几个核心概念，它们在JavaScript中都有相应的实现方式。了解和掌握这些概念对于进行复杂的面向对象编程至关重要。

### 构造函数
构造函数主要用来创建对象，并为对象的成员赋初始值
#### 三种创建对象方式
1.利用`new Object()`创建对象
```javascript
var obj = new Object();
```
2.利用`对象字面量`创建对象
```javascript
var obj2 = {};
```
3.利用`构造函数`的实例化创建对象
```javascript
// 构造函数中的属性和方法成为成员，成员可以添加
// 构造函数创建对象
function Star(uname,age){
  // 属性 实例成员
  this uname = uname;
  this age = age;
  // 方法 类成员
  this.sing = function(){
    console.log('我会唱歌')
  }
}
// 实例化对象
var ldh = new Star('刘德华',18)
// 实例成员：构造函数内部的值或属性
// 类成员：构造函数中的方法

// 实例成员：构造函数内部通过this指向的成员uname age sing 就是实例成员
// 实例成员只能通过实例化的对象来访问，不能通过构造函数来访问

// 静态成员：在构造函数身上添加的成员 只能通过构造函数来访问
Star.sex = '男'
```

- 构造函数首字母要大写
- 需要使用`new`关键字

new 在执行时候会做4件事情：

1. 在内存中创建一个新的空对象
2. 让this指向这个新对象
3. 执行构造函数中的代码，给这个新对象添加属性和方法
4. 返回这个新对象（所以构造函数里里面的不需要使用return）

构造函数的缺点：浪费内存<br />4.利用class的实例化对象
```javascript
// es6后引入了class，本质上也是构造函数
class Person{
  constructor(name,age){
    this.name = name;
    this.age = age;
  }
}
const person1 = new Person('Mike',18);
console.log(person1.name);
console.log(person1.age)

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/28047720/1673430597288-6361d6ba-fd07-464f-be37-b16b1545a182.png#averageHue=%23f7faf7&clientId=ub4683000-1add-4&from=paste&height=536&id=ufd97faf3&originHeight=536&originWidth=1245&originalType=binary&ratio=1&rotation=0&showTitle=false&size=189435&status=done&style=none&taskId=ub7835dfc-2b12-43e1-8038-c8feaa0927d&title=&width=1245)<br />构造函数里的方法属于复杂数据类型，需要单独开辟内存空间，而每次实例化构造函数时都会给函数开辟新的空间，照成内存浪费
#### 原型对象prototype
原型对象prototype<br />对象原型__proto__<br />每一个构造函数中都有一个prototype属性，指向另一个对象<br />作用：共享方法<br />一般情况下，将`公共属性`定义到构造函数中（简单数据类型放到构造函数里面），`公共方法`（复杂数据类型）放到原型对象上
```javascript
function Star(uname,age){
  // 属性
  this uname = uname;
  this age = age;
}
// 往Star对象中添加sing方法
Star.prototype.sing =function(){
    console.log('我会唱歌')
}
var ldh = new Star('刘德华',18)
ldh.sing();
// 先看lgh身上有没有sing这个方法，如果有就执行
// 如果没有就会去创建它的构造函数上查找
```
对象身上会被系统添加一个__proto__指向构造函数的原型对象prototype<br />✨实例化对象.__proto__ === 构造函数.prototype
#### 构造函数
对象原型和原型对象里面都有一个 constructor 属性 ， constructor  我们称为构造函数，因为它指向构造函数本身，它用于记录改对象引用了那个构造函数<br />对象.__proto__ .constructor === 构造函数.prototype.constructor
```javascript
function Star(uname,age){
  // 属性
  this uname = uname;
  this age = age;
}
// 当公共的方法有很多的时候
// 可以以对象的形式进行添加到prototype上
Star.prototype = {
  // 如果修改了原型对象，就需要利用constructor指回原来的构造函数
  constructor:Star,
  sing:function(){
    console.log('我会唱歌')
  },
  movie:function(){
    console.log('演电影')
  }
}

var ldh = new Star('刘德华',18)
ldh.sing();
```
#### 构造函数和原型对象
![image.png](https://cdn.nlark.com/yuque/0/2023/png/28047720/1673435061978-737e821c-843e-42d7-ac65-75ace1fc2743.png#averageHue=%23fbfcfb&clientId=ub4683000-1add-4&from=paste&height=526&id=u1240f469&originHeight=526&originWidth=938&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112675&status=done&style=none&taskId=u3ecf4c63-df13-4482-9d2a-d38085fcb69&title=&width=938)<br />原型（Prototype）和原型链（Prototype Chain）是JavaScript中面向对象编程的基石之一。理解原型和原型链对于掌握JavaScript的继承和对象创建至关重要。

### 原型
在JavaScript中，每个对象都有一个内置的`__proto__`属性（在现代浏览器中，这个属性已经被`Object.getPrototypeOf()`所取代），指向它的原型对象。这个原型对象本身也是另一个对象，它可以有自己的属性和方法。原型对象也可以有自己的原型，形成一个原型链。<br />当你创建一个对象时，该对象会继承其构造函数的原型对象的属性和方法。原型对象可以是任何对象，包括`Object.prototype`，它是所有对象的原型祖先。<br />例如：
```javascript
const person = {
  name: 'Alice',
  greet: function() {
    console.log(`Hello, my name is ${this.name}.`);
  }
};
console.log(Object.getPrototypeOf(person)); // 输出： Object.prototype
```

在这个例子中，`person`对象的原型是`Object.prototype`。

### 原型链
当尝试访问一个对象的属性或方法时，如果该对象本身没有这个属性或方法，JavaScript引擎会沿着原型链向上查找，直到找到为止。这个过程称为原型链查询。<br />原型链的查找基于`__proto__`属性，它会一直向上追溯到`Object.prototype`。<br />例如：
```javascript
function Animal(name) {
  this.name = name;
}
Animal.prototype.speak = function() {
  console.log(`${this.name} makes a noise.`);
};
const dog = new Animal('Buddy');
dog.speak(); // 输出： Buddy makes a noise.
console.log(dog.__proto__ === Animal.prototype); // 输出： true
console.log(Animal.prototype.__proto__ === Object.prototype); // 输出： true
```
在这个例子中，`dog`对象的原型是`Animal.prototype`，而`Animal.prototype`的原型是`Object.prototype`。
### 原型链的工作原理
当访问`dog`对象的`speak`方法时，JavaScript引擎首先检查`dog`对象本身是否有`speak`方法。如果没有，它就会查找`dog`对象的原型`Animal.prototype`是否有`speak`方法。如果还是没有，就会继续查找`Animal.prototype`的原型`Object.prototype`，直到找到为止，或者如果所有的原型都没有这个方法，则会返回`undefined`。
### 原型链的优势
原型链是JavaScript实现继承的主要方式，它有以下优势：

1. 动态继承：对象继承另一个对象是动态的，不需要静态地定义类层次结构。
2. 节省内存：共享原型上的属性和方法，避免了在每个实例上重复创建它们。
3. 灵活性：可以随时修改原型对象，从而影响到所有基于该原型创建的对象。<br />了解原型和原型链对于编写高效、可维护的JavaScript代码至关重要。
## 原型与类
```javascript
代码function Star(uname,age){
  this uname = uname;
  this age = age;
}
Star.prototype.sing =function(){
    console.log('我会唱歌')
}
和
class Star(){
   constructor(uname,age){
        this.uname = uname;
        this.age = age;
}
    sing(){
      console.log('我会唱歌')
}有什么区别
```
你提供的两段代码分别使用了JavaScript的原型（prototype）模式和类（class）模式来定义一个`Star`构造函数和它的`sing`方法。下面是这两种模式的区别：

1. **原型模式（Prototype Pattern）**: 
- 在原型模式中，函数的`this`指向的是当前的实例。当你调用`new Star()`时，`uname`和`age`属性会直接添加到新创建的实例上。
- 原型模式中，方法是定义在`Star.prototype`上的，这意味着所有实例都会共享这个方法。
- 优点是如果实例需要相同的方法和属性，这可以减少内存的使用。
- 使用`this`来赋值属性和通过`Star.prototype`来定义方法是原型模式的特点。
2. **类模式（Class Pattern）**: 
- 在类模式中，`constructor`方法在每次使用`new`关键字调用类时都会被调用，`this`指向新创建的实例。
- 类模式中，方法和属性通过在类定义中声明的方式来实现，而不是通过原型。每个实例都会有它自己的方法和属性副本。
- 使用`constructor`方法来初始化实例的属性和通过类字段（class fields）或静态方法（static methods）来定义类级别的属性和方法是类模式的特点。<br />在这两种模式中，`sing`方法都是用来实现唱歌的行为，但是原型模式下所有实例共享一个`sing`方法，而在类模式下，每个实例都有自己的`sing`方法。<br />在现代JavaScript中，类模式是ECMAScript 6引入的新特性，它提供了一种更接近传统面向对象编程语法的方式。然而，原型模式依然在许多旧的JavaScript代码库和某些特定的应用场景中使用。<br />尽管类提供了更直观的语法和一些便利特性（如属性和方法的命名冲突检测），但原型模式在一些性能敏感的应用中仍然很有用，因为它避免了在每次实例化时复制方法。<br />根据你的需求，你可以选择最适合你的应用场景的模式。在编写现代JavaScript应用程序时，通常更倾向于使用类，因为它提供了更清晰的语法和更好的 TypeScript 支持。
## this指行
### 回流与重绘
#### 浏览器内核
![image.png](https://cdn.nlark.com/yuque/0/2023/png/28047720/1673507846662-c4c45243-9e79-4ee8-8636-a5ee34e4e8d6.png#averageHue=%23314456&clientId=uebb324c7-cc9d-4&from=paste&height=537&id=u3f392545&originHeight=537&originWidth=1015&originalType=binary&ratio=1&rotation=0&showTitle=false&size=404007&status=done&style=none&taskId=ud695d053-2415-4897-814e-8d4947eea56&title=&width=1015)
#### 浏览器渲染机制
浏览器采用流式布局模型<br />将HTML解析为DOM，把CSS解析成CSSOM，把CSSOM与DOM结合生成render  tree<br />有了render tree 之后，就会计算节点的位置，然后把节点绘制到页面上<br />浮动脱离流式布局
#### 回流 reflow
元素的结构或位置发生改变，浏览器重新渲染部分或全部文档的过程中叫做回流<br />示例：首次渲染页面，浏览器窗口大小发生变化，内容变化，添加或者删除节点，激活css伪类，display:none
#### 重绘 repaint
当页面按中元素样式的改变不影响它在文档流中的位置，浏览器会将新样式赋予元素，这个过程叫做重绘

#### 总结
回流性能消耗比重绘大，<br />css避免使用table布局，避免设置多层内联样式<br />js避免频繁操作DOM，对于大量操作DOM的操作建议使用文档片段<br />回流一定会引起重绘，重绘不一定回流

### 闭包
执行上下文：创建阶段、执行阶段 
### this
this的4种绑定规则
```javascript
// 函数被调用的时候，this默认指向全局Window对象
function girl(){
  console.log(this);
}
girl();		//output:		Window
```
```javascript
// 调用对象方法时出现隐式绑定
var girl = {
  name:"Amy",
  height:160,
  detail:function(){
  console.log('姓名'+ this.name);
  console.log('身高'+ this.height);
  }
}
girl.detail()
```
```javascript
// 硬绑定
var girlName = {
  name:"小红",
  sayName:function(){
    console.log('我的女朋友是'+this.name)
  }
  var girl1 = {
    name:"小白"
  }
	var girl2 = {
    name:"小黄"
  }
}
girlName.sayName.apply(girl1);	//output:		小白
girlName.sayName.apply(girl2);	//output:		小黄
```
```javascript
// 构造函数绑定
function Lover(name){
  this.name = name;
  this.sayName = function(){
    console.log('我的老婆是'+ this.name);
  }
}
var name = '小白'
var xiaoHong = new Lover('小红');
xiaoHong.sayName();		//output:		小红
```
题目<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/28047720/1673518952950-0ddab3d2-a034-4591-9c27-158bd76b839c.png#averageHue=%23aa9a8c&clientId=uebb324c7-cc9d-4&from=paste&height=654&id=u48627538&originHeight=654&originWidth=1617&originalType=binary&ratio=1&rotation=0&showTitle=false&size=278892&status=done&style=none&taskId=ud0e822c2-3c3d-4b37-a783-a7fd19cc95b&title=&width=1617)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/28047720/1673519076916-2b49e95f-2223-4a68-9a4a-403ddacc9c9e.png#averageHue=%23504839&clientId=uebb324c7-cc9d-4&from=paste&height=924&id=u37649c90&originHeight=924&originWidth=1357&originalType=binary&ratio=1&rotation=0&showTitle=false&size=375015&status=done&style=none&taskId=u9628c1cc-1d9b-4a90-8314-1f547cdc97f&title=&width=1357)
### Javascript Event Loop
JavaScript是一个单线程语言，每次只有一个主线程执行代码，然而 JavaScript 却又是一个非阻塞（Non-blocking）、异步（Asynchronous）、并发式（Concurrent）的编程语言<br />**事件循环（Event Loop）** 是让 JavaScript 做到既是**单线程**，又绝对**不会阻塞**的核心机制，也是 JavaScript **并发模型（**[Concurrency Model](https://link.zhihu.com/?target=https%3A//developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)**）**的基础，是用来协调各种事件、用户交互、脚本执行、UI 渲染、网络请求等的一种机制。<br />Event Loop 分为两种 Browsing Context 和 Worker

- Browsing Context用于将Document展现给用户的环境

Event Loop由三部分组成<br />调用栈（call stack）<br />消息队列（Messaqe Queue）<br />微任务队列（Microtask Queue）<br />执行机制<br />遇到函数调用时，会把函数调用压入调用栈中，被压入的函数叫做帧（farme）<br />微任务队列会在最后一个函数弹出栈后立即执行（比消息队列先执行）
### 回调函数
自己的理解：<br />将函数B作为一个参数传入函数A，当函数A（主函数）执行完成后再去执行函数B，这个过程就叫做回调，而函数B叫做回调函数<br />在js中，函数可以当作参数进行传递
```javascript
function first(a){
  console.log('First');
  //回调函数
  a();
}
function second(){
  console.log('Second')
}

first(second);
```
**回调函数解决异步中任务执行顺序问题**<br />在JavaScript中，异步任务的执行顺序是不确定的，因为它们是在事件循环中执行的。为了解决这个问题，我们可以使用回调函数来确保任务按照我们期望的顺序执行。<br />例如，假设我们有两个异步函数A和B，我们希望在A完成后执行B。我们可以将B作为A的回调函数传递给A，这样当A完成后，它会自动调用B。<br />下面是一个示例代码：
```
function A(callback) {
  // 异步操作
  setTimeout(function() {
    console.log('A完成');
    callback();
  }, 1000);
}

function B() {
  console.log('B完成');
}

A(B);
```

在这个例子中，函数A是一个异步函数，它接受一个回调函数作为参数。在A完成后，它会调用回调函数。函数B是我们想要在A完成后执行的函数。我们将B作为回调函数传递给A，这样当A完成后，它会自动调用B。

不是所有的回调函数都是异步操作
```javascript
let arr = [1,2,3]
arr.map((item)=>{
  console.log(item)
})
console.log("Hi")
// output:		1		2		3		Hi
```
### 定时器
#### setInterval()
每等待一个时间间隔都执行一次<br />此函数具有一个返回值`interval ID`,该id代表为定时器标识，可用作 clearInterval() 方法的参数。
#### setTimeout
等待时间，然后只执行一次
### js异步编程
#### 同步 
一部接着一部完成（事情按顺序一件一件完成）
#### 异步
属于异步操作的有：事件，setTimeout，setInterval，网络请求等<br />异步操作要等到主线程完成后才执行<br />异步的解决方案是事件轮询<br />异步加载图片
```javascript
function loadImag(src){
  let img = new Image();
  img.src = src;
}
loadImag('img/xx.png');
console.log('Hello')
// 效果：先输出Hello 然后再加载图片
```
任务排列
#### 回调函数实现异步
回调<br />一个函数被作为一个参数传递到另一个函数里，在那个函数执行完后再执行。
```javascript
function A(callback){
    console.log("I am A");
    callback();  //调用该函数
}
 
function B(){
   console.log("I am B");
}

// 调用函数a，此时function B作为一个参数传入 function A
// 所以function B 是function A 的回调函数
A(B);
```
同步回调<br />上面解释回调函数的例子就是同步回调<br />异步回调
```javascript
var xhr= new XMLHttpRequest(),
    method = "GET",
    url = "https://developer.mozilla.org/";

xhr.open(method, url, true);
xhr.onreadystatechange = function () {
  if(xhr.readyState === XMLHttpRequest.DONE && xhr.status === 200) {
    console.log(xhr.responseText)
  }
}
xhr.send();

```
[XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest) 的[readyState](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState) 属性发生改变时触发 [readystatechange](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/readystatechange_event) 事件的时候被调用，每一次变化就触发一次onreadystatechange 函数，进行判断是否正确拿到返回结果<br />样例<br />现在有三个函数 `fun1,fun2和fun3`,`fun1`是一个耗费时间的操作，而`fun2`是需要在`fun1`后执行的函数，为了不影响`fun3`的执行，我们可以把`fun2`写成`fun3`的回调函数。
```javascript
function fun1(callback) {
setTimeout(() => {
    console.log("我是方法fun1");
    callback();
  }, 1000);
}
function fun2() {
  console.log("我是方法fun2");
}
function fun3() {
  console.log("我是方法fun3");
}

fun1(fun2);
fun3()
// 输出 我是方法fun3		我是方法fun1		我是方法fun2
```
#### Promise

- promise 是一个**构造函数**
- Promise 的构造函数接收一个函数为参数，并且传入两个参数：**resolve**，**reject**，分别表示异步操作执行成功后的回调函数和异步操作执行失败后的回调函数。 
- Promise创建后状态为`pending`  resolve会将Promise状态变为`fulfilled`  reject会将Promise状态变为`rejected`
- 只有在 Promise状态发生改变之后，才会执行`then`方法
```javascript
var promisse = new Promise(function(resolve,reject){
  if(/* 操作成功 */){
    resolve('success')
  } else{
    reject('fail')
  }
})

// 当promise状态发生改变时（pending状态变为fulfiled或者rejected）都会执行then()
// then 为 微任务
promise.then(function(res){
  console.log('res')
}).catch((err)=>{
  console.log(err)
})
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/28047720/1675928554099-abd9686d-091b-4558-a92b-70c0f3b9cbf8.png#averageHue=%23343744&clientId=ucbc57fd8-0e1d-4&from=paste&height=708&id=ubea3fbfb&originHeight=708&originWidth=1062&originalType=binary&ratio=1&rotation=0&showTitle=false&size=306034&status=done&style=none&taskId=ub429e65a-5251-478a-bd7a-fcffe87118b&title=&width=1062)<br />Promise三种重要状态<br />Pending 准备状态<br />Resloved 成功状态<br />Rejected 拒绝状态<br />✨setTimeout 产生宏任务<br />✨Promise 产生微任务  <br />🚨Promise 构造函数中的代码也是同步代码<br />🚨Promise 状态不变时，then中方法不会执行<br />🚨Promise 状态发生改变时`.then`方法中的代码添加到微任务队列<br />微任务队列<br />宏任务队列 <br />执行权重  同步》微任务》宏任务
### 任务优先级
同步立刻执行 <br />同步执行完后才会执行微任务队列-<br />主线程中的任务执行完成后，才会去轮询微任务和宏任务<br />执行顺序：同步 > 微任务(Promise) > 宏任务<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/28047720/1683870621809-17b30aba-9809-4b22-9162-4bff6035482c.png#averageHue=%2329353b&clientId=uc31c084f-ad43-4&from=paste&height=813&id=ueb51a0f4&originHeight=813&originWidth=1617&originalType=binary&ratio=1&rotation=0&showTitle=false&size=383569&status=done&style=none&taskId=u933942b8-dbe8-4984-a692-7556c91b53e&title=&width=1617)
### 状态中转
Promise的状态能传递给下一个Promise
### async...await
```javascript
async get(name){
  let respone = await ajax('https://developer.mozilla.org/')
  console.log('Hello');
  return user
}
// 在给方法加上async标记，然后内部原来是异步的操作加上await标记后，
// 在遇到耗时操作时（原本会产生异步的操作），就会先等待该耗时操作完成，再接着执行代码
```
# 设计模式
## 构造器模式
```javascript
function Employee(name,age){
  this.name = name;
  this.age = age;
  this.say = function(){
    console.log(hthis.name+'-',this.age)
  }
}
// 每次创建对象都会在内存中开辟新的空间，由此实现对象与对象之间的独立
var employee1 = new Employee("Mike",100)
var employee2 = new Employee("Jack",200)
```
## 原型模式
```javascript
function Employee(name,age){
  this.name = name;
  this.age = age;
}
// 将共同的方法放到原型上，实现方法共用一个内存空间
// 防止对象创建时，方法占用内存空间
Employee.prototype.say = function(){
    console.log(this.name+'-',this.age)
}


// class构造器
class Employee2{
  constructor(name,age){
    this.name = name;
    this.age = age;
  }
  say() = function(){
    console.log(this.name+'-',this.age)
  }
}

// new会生成类的实例，然后使用this关键字指向实例
```
# 异步使用总结
## 总结

- 箭头函数不能使用`async`进行标记，如果要使用async/await语法糖，被标记方法只能是普通函数或匿名函数
- async/await 用于获取 promise执行结果(resloce/reject) 的返回值, 若没有return promise对象 或 执行结果没有返回值，则结果undefined （详细见await获取结果）
- 旦 Promise 的状态确定（即已经变为 resolved 或 rejected），就无法再次修改它的状态。一旦 Promise 进入 resolved 状态，它的值就被固定下来，而一旦进入 rejected 状态，它的错误原因也被固定下来。在这之后，无论后续链式调用中发生什么操作，都不会再改变 Promise 的状态。
- 在promise链式调用中，只需要一个catch方法就能捕获到整个链条中的错误
## promise错误处理
```javascript
let proText = data => {
    return new Promise((resolve, reject) => {
        console.log('输出传入的data');
        reject(data);
    })
        .then(res => {
            console.log('===promise的结果为成功===');
            return res;
        })
        .catch(err => {
            console.log('===promise的结果为失败===');
            return err;
        });
};
// 调用
let temp_data = await proText('传入的测试数据');
```
## await获取结果
```javascript
let promise1 = data => {
    return new Promise((resolve, reject) => {
        console.log('=== First Promise ===');
        reject(data);
    })
        .then(res => {
            console.log('First Promise Success');
            return res;
        })
        .catch(err => {
            console.log('First Promise Error');
            console.log(err);
        });
};

let promise2 = (resp, data) => {
    return new Promise((resolve, reject) => {
        console.log('=== Second Promise ===');
        resolve(data);
    })
        .then(res => {
            res = resp + ' ' + res;
            console.log('Second Promise Success');
            return res;
        })
        .catch(err => {
            console.log('Second Promise Error');
            console.log(err);
        });
};

async function runLoop() {
    let res = await promise1('promise1');
    console.log(res);
    let res2 = await promise2(res, 'promise2');
    console.log(res2);
}
runLoop();
```
## promise链式调用

