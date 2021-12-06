### 	 1、数据类型

1. 基本数据类型
   - String
   - Boolean
   - Number
   - undefined         表示变量声明但未初始化时的值 
   - null                     表示一个空对象指针
2. 引用数据类型
   - Object
   - Array
   - Function

*Symbol 是 ES6 引入了一种新的原始数据类型，表示独一无二的值。*

### 2、判断数据类型

1. typeof                               判断原始数据类型   数组、对象、null都会被判断为object，其他判断都正确
2. instanceOf                      不能用于判断原始数据类型的数据      **只能正确判断引用数据类型**
3. Object.prototype.toString.call(2)       ->Number
4. constructor  => Object            __proto__  =>   String.prot            通过原型链来判断
5. 判断是否为 null  =>           ===      Object.prototype.toString.call()

> 判断数组 

1. Object.prototype.toString.call(obj).slice(8,-1) == 'Array'
2. Array.isArray(value)           可以用来判断 value 是否是数组
3. Array.prototype.isPrototypeOf(obj)   判断是否为数组
4. arr.__ proto__ Array.prototype      原型链判断

~~~javascript
typeof undefined // "undefined" 
typeof null     // "object"
typeof 1      // "number

3 instanceof Number // false
var date = new Date() 
date instanceof Date // true 
var number = new Number() 
number instanceof Number // true

Object.prototype.toString.call('845')   // [object String]

const a = 4
a.constructor == Number //true
~~~

###  3、创建对象

1. 字面量对象   =>  默认这个对象的原型链指向 object
2. new Object ()  声明一个对象
3. 构造函数创建对象
4. Object.create

~~~javascript
const o = {}
const o = new Object({name:'o3'})
const o = function(){
    this.name = 'haha'
} 
var P = {name:'o3'};
const o = Object.create(p) 
~~~

### 4、创建函数

~~~javascript
const a = function(){}
function fn (){}
const fn = new Function('参数1','参数2', "表达式")
~~~

 ### 5、继承

~~~javascript
function father(){
    this.name = '小明'
}
function son(){
	father.call(this)
}
~~~

1. 如何理解this关键字
2. call apply bind 基本语法
3. new 关键字做了什么
4. JavaScript 运行机制(单线程)   事件循环  
5. JavaScript 循行机制  宏任务  微任务
6. promise  async await 的理解
7. 闭包
8. 拷贝
9. 防抖和节流
10. 原型对象和原型链

### 6、如何理解this关键字

1. 在全局中this指向的是window
2. 在对象方法中this指向的调用方法的对象
3. 在事件对象中this，指向的是触发事件的DOM对象
4. 构造函数中的this，指向的是new创建的实例化对象
6. 内部函数中的this  ,指向的是全局对象
7. 箭头函数没有自己的this ，指向定义函数上下文的this
8. 使用闭包，var获取dom 的索引

### 7、call apply bind的用法

1. 调用函数
2. 可以改变this 的指向
3. call(this,参数1,参数2 ....)
4. apply(this,[参数1,参数2 ....])
5. bind() 改变this 指向 不调用函数

### 8、new的理解

1. 创建一个空对象
2. 设置原型，将对象的原型设置为函数的 prototype 对象。
3. 将this指向空对象    动态给刚创建的对象添加成员属性                                                                                                                                                                                                                                                                                                                                                                  
4. 隐式返回 this

~~~javascript
function person(name,age){
	this.name = name;
    this.age = age
}
//let obj = new person('小明',20)

const obj = {}  
obj.__proto__ = person.prototype;
person.call(obj,'小红',53);


~~~

### 9、JavaScript运行机制

1. 同步 : 顺序执行代码
2. 异步  ：定时器  ajax   读取文件
   1. 宏任务
   2. 微任务   promise.then
3. 执行顺序 ： 同步任务 =>  process.nextTick => 微任务 => 宏任务 => setImmediate

~~~javascript
console.log('同步代码');
setTimeOut(()=>{
    console.log('同步代码执行完成  异步代码执行' )
},0)

new Promise((resolve,resject) => {
    resolve(res)
	console.log('同步代码')
}).then(res => {
	异步代码
})

~~~

### 10、理解promise  async 







### 11、闭包(closure)

> 函数嵌套函数  内部函数就是闭包

- 优点：
  - 避免全局变量的污染
  - 变量存在内存中不会被销毁
- 缺点
  - 滥用闭包消耗内存

~~~javascript
function outerFun(){
    let a =  '闭包'
    function innerFun(){
		console.log(a)
    }
    return innerFun
}

　var name = "The Window";
　　var object = {
　　　　name : "My Object",

　　　　getNameFunc : function(){
        //var that = this      使用闭包
　　　　　　return function(){
          	 //return that.name
　　　　　　　　return this.name;
　　　　　　};

　　　　}

　　};
console.log(object.getNameFunc()())     //The Window 

~~~

### 12、对象的浅(深)拷贝

~~~javascript
//浅拷贝
const obj = {
    name:'小明',
    age:88
}
const cloneobj = {}
for(var key in obj){
	cloneobj[key] = obj[key]
}
//assgin 浅拷贝语法糖
const obj = {
    name:'小明',
	age:88
}
const o ={}
Object.assgin(o,obj)


//深拷贝
const deepClone(source){
	let result = Array.isArray(source) ? [] :{}
    if(typeof source == 'object'){
		for(var key in source){
			if(typeof source[key] =='object' ){
				result[key] = deepClone(source[key])
            }else{
				result[key] = source[key]
            }
        }	
    }
    return result
}

function deepCope(source){
    let res = Json.parse(Json.Stringif(source))
    return res
}
~~~





