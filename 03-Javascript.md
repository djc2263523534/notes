### 重点:

|    方法名     | 对应版本 |                             功能                             | 原数组是否改变 |
| :-----------: | :------: | :----------------------------------------------------------: | :------------: |
|   concat()    |   ES5-   |                合并数组，并返回合并之后的数据                |       n        |
|    join()     |   ES5-   |              使用分隔符，将数组转为字符串并返回              |       n        |
|     pop()     |   ES5-   |                删除最后一位，并返回删除的数据                |       y        |
|    shift()    |   ES5-   |                 删除第一位，并返回删除的数据                 |       y        |
|   unshift()   |   ES5-   |              在第一位新增一或多个数据，返回长度              |       y        |
|    push()     |   ES5-   |             在最后一位新增一或多个数据，返回长度             |       y        |
|   reverse()   |   ES5-   |                      反转数组，返回结果                      |       y        |
|    slice()    |   ES5-   |                  截取指定位置的数组，并返回                  |       n        |
|    sort()     |   ES5-   |                  排序（字符规则），返回结果                  |       y        |
|   splice()    |   ES5-   |             删除指定位置，并替换，返回删除的数据             |       y        |
|  toString()   |   ES5-   |                    直接转为字符串，并返回                    |       n        |
|   valueOf()   |   ES5-   |                     返回数组对象的原始值                     |       n        |
|   indexOf()   |   ES5    |                     查询并返回数据的索引                     |       n        |
| lastIndexOf() |   ES5    |                   反向查询并返回数据的索引                   |       n        |
|   forEach()   |   ES5    | 参数为回调函数 会遍历数组所有的项 回调函数接受三个参数 分别为value，index，self；forEach没有返回值 |       n        |
|     map()     |   ES5    |     同forEach，同时回调函数返回数据，组成新数组由map返回     |       n        |
|   filter()    |   ES5    | 同forEach，同时回调函数返回布尔值，为true的数据组成新数组由filter返回 |       n        |
|    every()    |   ES5    | 同forEach，同时回调函数返回布尔值，全部为true，由every返回true |       n        |
|    some()     |   ES5    | 同forEach，同时回调函数返回布尔值，只要由一个为true，由some返回true |       n        |
|   reduce()    |   ES5    | 归并，同forEach，迭代数组的所有项，并构建一个最终值，由reduce返回 |       n        |
| reduceRight() |   ES5    | 反向归并 同forEach，迭代数组的所有项，并构建一个最终值，由reduceRight返回 |       n        |

### :star:Array

### 1、转换字符串

1. join()：用指定的分隔符将数组每一项拼接为字符串
2. toString():将数组转换为字符串
3. toLocaleString() 方法可把一个 Number 对象转换为本地格式的字符串

~~~javascript
 1.toString()
const arr = ['a', 'b', 'c']
 const str = arr.toString()
 console.log(str);  // a,b,c

2.join()
const arr = ['a', 'b', 'c']
const str = arr.join('|')
console.log(str);  // a|b|c

3.toLocaleString()
const arr = ['a', 'b', 'c']
const str = arr.toLocaleString('')
console.log(str);    //a,b,c
~~~

### 2、类数组转换

1. Array.prototype.splice.call(arrayLike)
2. Array.prototype.slice.call(arrayLike , 0)
3. Array.prototype.cocat.apply([] , arrayLike)
4. Array.from(arrayLike)

### 3、增删改查

1. push() ：向数组的末尾添加新元素
2. unshift()：向数组首位添加新元素
3. pop()：删除数组的最后一项
4. shift()：删除数组的第一项
5. splice (添加或者删除的位置,删除位数,添加的元素)：对数组进行增删改  
6. concat()：用于连接两个或多个数组

~~~javascript
1.增
const arr = ['a', 'b', 'c']
arr.push('d')
arr.unshft('z')
console.log(arr);    //[z,a,b,c,d]     

2.删
const arr = ['a', 'b', 'c']
arr.pop()
arr.shift()
console.log(arr);  //  ['b']

3.增和删
const arr = ['a', 'b', 'c']
arr.splice(0, 2, 'e', 'f', 'g')
console.log(arr);  //['e','f','g','c']

4.连接
const arr1 = ['a','b']
const arr2 =['c','d']
const arr3 = arr1.concat(arr2) //['a','b','c','d']
~~~

### 4、截取元素

1. slice()：按照条件查找出其中的部分元素  
2. splice(截取位置，截取位数)

~~~javascript
1.slice()截取
const arr = ['a', 'b', 'c']
const arr1 = arr.slice(1)  // ['b','c']
const arr3 = arr.slice(0, 2)  // ['a',b]

2.splice()用法
const arr = ['a','b','c']
const arr = arr.splice(0,2)  //[a,b]
~~~

### 5、索引和位置

1. indexOf(value)：检测当前值在数组中第一次出现的位置索引(未查询到返回-1)
2. lastIndexOf(value)：检测当前值在数组中最后一次出现的位置索引(元素最后一个值的索引)
3. reverse()：对数组进行倒序
4. sort()：对数组的元素进行排序

~~~javascript
1.indexof首次出现
const arr = ['a','b','c','d']
console.log(arr.indexOf('d'))   //返回索引3

2.lastIndexOf最后的元素
const arr = ['a', 'b', 'c', 'd']
console.log(arr.lastIndexOf('c'))  //3

const arr = ['a', 'b', 'b', 'c',]
console.log(arr.lastIndexOf('b'));  //2

3.翻转
const arr = ['a', 'b', 'c', 'd']
console.log(arr.reverse()); // ['d','c','b',a]

4.排序
const arr = [11, 6, 9, 2]
console.log(arr.sort((a, b) => a - b));  [2,6,9,11]
~~~

### 6、方法

1. forEach()：ES5 及以下循环遍历数组每一项
2. map()：ES6 循环遍历数组每一项  实际效率还比不上forEach
3. filter():“过滤”功能
4. every()：判断数组中每一项都是否满足条件(每个满足为true)
5. some()：判断数组中是否存在满足条件的项(单个满足为true)

~~~javascript
1.forEach  map
const arr = ['a', 'b', 'c']
arr.forEach((value, index, arr) => {
console.log(value);
})

2.过滤
const arr = ['1', '2', '3']
const arr1 = arr.filter((value, index, arr) => value > 1)
console.log(arr1);  // ['2','3']

3.条件判断
const arr = ['1', '2', '3']
const arr1 = arr.every((value, index, arr) => value > 1)
console.log(arr1);  // false

const arr2 = arr.some((value, index, arr) => value > 1)
console.log(arr2);  // true
~~~

1. find():返回匹配的值(返回一个值)
2. findIndex():返回匹配位置的索引
3. reduce()   
4. includes()：判断一个数组是否包含一个指定的值
5. flat()、flatMap()：扁平化数组

~~~javascript
1.查找
const arr = ['1', '2', '3']
const arr1 = arr.find((value, index, arr) => value == 2)
console.log(arr1);  // 2

2.索引
const arr = ['a', 'b', 'c']
const arr1 = arr.findIndex((value, index, arr) => value == 'c')
console.log(arr1);   // 返回索引3

3.计算
const arr = [1, 2, 3]
const arr1 = arr.reduce((prevalue, value) => prevalue + value)
console.log(arr1);

4.判断
const arr = ['a','b','c']
arr.includes('a')  //返回boolean值

5.扁平化数组
const arr = ['1', '2', '3', ['1', '2', '3', ['1', '2', '3']]]
const arr1 = arr.flat(2)
console.log(arr1);
案例1:
var arr1 = [1, 2, 3, 4];
arr1.map(x => [x * 2]);    // [[2], [4], [6], [8]]
arr1.flatMap(x => [x * 2]);  // [2, 4, 6, 8]
案例2:
const arr = [['a'], ['b'], 3]
const arr1 = arr.flatMap((value) => value)
console.log(arr1);
~~~

1. copyWithin(复制到指定, 起始位置, end): 用于从数组的指定位置拷贝元素到数组的另一个指定位置中
2. entries() 、keys() 、values() :遍历数组




~~~javascript
1.conyWithin()
const arr = ['a', 'b', 'c', 'd']
const arr1 = arr.copyWithin(2, 0, 2)
console.log(arr1);  //['a','b','a','b']

2.entries遍历
const arr = ['a', 'b', 'b', 'c',]
const value = arr.entries()
console.log(value.next().value);   //[0, "a"]
console.log(value.next().value);   //[1, 'b']

2.values
const array1 = ['a', 'b', 'c'];
const iterator = array1.values();
for (const value of iterator) {
  console.log(value);     // a b c
}

3.keys
const array1 = ['a', 'b', 'c'];
const iterator = array1.keys();
for (const key of iterator) {
  console.log(key);   //打印索引 0 1 2
}
~~~

### :star:String

### 1、截取字符串

1. slice(start, end)  
2. substr(start, [length])
3. substring([from], to)

~~~javascript
1.slice
const str = 'baby'
const newStr = str.slice(1,3)  //ab

2.subtr
const str = 'baby'
const newStr = str.substr(1,3)  //aby

3.substring
const str = 'baby'
const newStr = str.substring(1,3)  // ab
~~~

### 2、索引

1. indexOf(substr, [start])         返回字符串中搜索到的字符或子字符串的索引。如果没有找到，则返回-1
2. lastIndexOf(substr, [start]) 
3. charAt(x)                          返回字符串中x位置的字符，下标从 0 开始。
4. charCodeAt(x) 					  返回字符串中x位置处字符的unicode值。  

~~~javascript
1.indexOf
const str = 'baby'
const newStr = str.indexOf('b')  // 索引0

2.lastindexOf
const str = 'baby'
const newStr = str.indexOf('b')  // 索引2

3.charAt
const str = 'baby'
const newStr = str.charAt(1)  // 字符串 a

4.charCodeAt
const str = 'baby'
const newStr = str.charCodeAt(1)  //unicode值 97
~~~

### 3、转换

1. toLowerCase()         字符串转换为小写
2. toUpperCase()          字符串转换为大写
3. split(delimiter, [limit])    可选的“limit”是一个整数，允许各位指定要返回的最大数组的元素个数
4. repeat()				             指定数量的字符串的副本
5. concat(v1,v2..)                  连接两个或多个字符串，此方法不改变现有的字符串，返回拼接后的新的字符串
6. trim()   去除两边空格

~~~javascript
1. 转小写
const str = 'ABC'
const newStr = str.toLowerCase()  // 'abc'

2.转大写
const str = 'abc'
const newStr = str.toUpperCase()  'ABC'

3.转数组
const str ='abc'
const arr = str.split('') // ['a','b','c']

4.复制
const str = 'abc'
const newstr = str.repeat(2)  //'abcabc'

2.连接
const str = 'abc'
const newstr = str.concat('def')  //'abcdef'
~~~

### 4、判断

1. includes()				用于检C:\Users\坟场蹦迪\Desktop\blogs\backend\mock\study.js C:\Users\坟场蹦迪\Desktop\blogs\backend\app.js查字符串是否包含指定的字符串或字符
2. endsWith()				字符串是否以指定的字符串或字符结束
3. stratsWith()

~~~javascript
1.includes
const str = 'abc'
const newstr = str.inclues('a')  //true

2.endsWith
const str = 'abc'
const newstr = str.endWith('c')  //true

3.stratWith
const str = 'abc'
const newstr = str.startWith('a')  //true
~~~

### 5.查询(正则)

1. replace(regexp/substr, replacetext)       用于一些字符替换另一些字符，或替换一个与正则表达式匹配的子串
2. match(regexp)            根据正则表达式在字符串中搜索匹配项。如果没有找到匹配项，则返回一个信息数组或null
3. search(regexp)



~~~javascript
1.replace
const str = 'abcahaia'
const newstr = str.replace(/a/gi, 'z')  // 'zbczhziz'

2.match
var str = "1 plus 2 equal 3"
const newstr = str.match(/\d+/g)      // ["1", "2", "3"]

3.search返回索引
var str="Visit Runoob!"; 
var n=str.search("Runoob");     // 索引6


valueOf()				返回一个String对象的原始值
fromCharcode(c1,c2)        转换一组Unicode值转换为字符。
~~~

### :star: Object 

### 1.获取值

1. Object.values()    获取对象所有值
2. Object.keys()     返回一个包含所有给定对象自身可枚举属性名称的数组。
3. Object.entries()   返回给定对象自身可枚举属性的[key, value]数组。

~~~javascript
1.获取值
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.values(obj)); // ['a', 'b', 'c']

2.获取属性名
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.keys(obj)); //  ['0', '1', '2']

3.获取组成值数组
const object1 = { foo: 'bar', baz: 42 };
console.log(Object.entries(object1)[1]);
// expected output: Array ["baz", 42]

~~~

### 2.创建和拷贝

1. Object.assign(目标,需要复制的对象)            通过复制一个或多个对象来创建一个新的对象
2. Object.create()           使用指定的原型对象和属性创建一个新对象
3. Object.defineProperty()         给对象添加一个属性并指定该属性的配置
4. Object.defineProperties()         给对象添加多个属性并分别指定它们的配置

~~~javascript
1.浅拷贝
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };
const returnedTarget = Object.assign(target, source);
console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }
console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }

2.创建
const person = {
  isHuman: false,
  printIntroduction: function () {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  }
};
const me = Object.create(person);

3.defineProperty
var obj = {  uname: '刘德华' , age: 20 , sex: '男'}
        // 添加或者修改对象 value writable enumerable configurable
        Object.defineProperty(obj, 'num', {
            value: 200
        })
        //不允许修改
        Object.defineProperty(obj, 'age', {
            writable: false,    //不允许修改 false
            enumerable: false,  //不允许遍历
            configurable: false   //不允许删除对象的某个元素
        })
        // obj.age = 0;
        // console.log(Object.keys(obj));
        delete obj.age
        console.log(obj);

4.defineProperties
var obj = {};
Object.defineProperties(obj, {
  'property1': {
    value: true,
    writable: true
  },
  'property2': {
    value: 'Hello',
    writable: false
  }
~~~

### 3.判断和冻结

1. Object.is()          比较两个值是否相同。所有 NaN 值都相等（这与==和===不同）

2. Object.freeze()            冻结对象：其他代码不能删除或更改任何属性。

3. Object.isFrozen()             判断对象是否已经冻结。

4. Object.isExtensible()          判断对象是否可扩展

5. Object.isSealed()             判断对象是否已经密封。

6. Object.hasOwnProperty( ) 检查属性是否被继承 

7. Object.isPrototypeOf( ) 一个对象是否是另一个对象的原型

   

### :star:Regexp

### 1、判断正则

1. test 检测正则
2. reg.exec  返回对象

~~~javascript
1.test 检测正则
const reg = /\d/g
reg.test(5) ///true

2.reg.exec  返回对象
let arr = ['哈哈k', 'pp哈哈', 'as哈哈a哈']
let res = arr.filter(item => item.match(/哈/gi))

3.str.match(reg)
~~~





### ⭐️Javascript

### 1.js注释

1. 单行注释  CTRL + /
2. 多行注释 shift + alt + A

### 2.数据类型

1. **基本类型**：字符串（String）、数字(Number)、布尔(Boolean)、对空（Null）、未定义（Undefined）、Symbol
2. **引用数据类型**：对象(Object)、数组(Array)、函数(Function)
3. isNaN()  检测是否为一个非数值         typeof 检测数据类型     instanceof     Array.isArray()
4. **转换为字符串**： 变量.toString()       String(变量)
5. **转换为数值型** ：parseInt() 整数型      parseFlost() 浮点型     Number()  数值型      ( - * / ) 隐式转换

### 3.运算符

1. 比较运算符
2. 逻辑运算符  &&  ||   !     逻辑中断 ：如果表达式一为真 则返回表达式二  
3. 赋值运算符
4. 小括号 一元 算数 关系 相等 逻辑 赋值 逗号 (运算符优先级)

### 4.流程控制

1. 分支结构：if(){}  if(){}else if(){}else{}                 switch(){ case value1: 执行代码 break; }
2. 三元表达式：？ ：
3. 循环结构：for(){}  while(true){}   do{}while(true)            continue  终止本次   break 当前



### 6.数字

1. toString() 以字符串返回数值
2. toFixed() 返回字符串值，它包含了指定位数小数的数字

| 方法         | 描述                         |
| :----------- | :--------------------------- |
| Number()     | 返回数字，由其参数转换而来。 |
| parseFloat() | 解析其参数并返回浮点数。     |
| parseInt()   | 解析其参数并返回整数。       |

| MAX_VALUE         | 返回 JavaScript 中可能的最大数。 |
| ----------------- | -------------------------------- |
| MIN_VALUE         | 返回 JavaScript 中可能的最小数。 |
| NEGATIVE_INFINITY | 表示负的无穷大（溢出返回）。     |
| NaN               | 表示非数字值（"Not-a-Number"）。 |
| POSITIVE_INFINITY | 表示无穷大（溢出返回）。         |



### 7.日期

1. new date()

| 方法              | 描述                                 |
| :---------------- | :----------------------------------- |
| getDate()         | 以数值返回天（1-31）                 |
| getDay()          | 以数值获取周名（0-6）                |
| getFullYear()     | 获取四位的年（yyyy）                 |
| getHours()        | 获取小时（0-23）                     |
| getMilliseconds() | 获取毫秒（0-999）                    |
| getMinutes()      | 获取分（0-59）                       |
| getMonth()        | 获取月（0-11）                       |
| getSeconds()      | 获取秒（0-59）                       |
| getTime()         | 获取时间（从 1970 年 1 月 1 日至今） |

### 9、Math

| 方法             | 描述                                                     |
| :--------------- | :------------------------------------------------------- |
| abs(x)           | 返回 x 的绝对值                                          |
| acos(x)          | 返回 x 的反余弦值，以弧度计                              |
| asin(x)          | 返回 x 的反正弦值，以弧度计                              |
| atan(x)          | 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。 |
| atan2(y,x)       | 返回从 x 轴到点 (x,y) 的角度                             |
| ceil(x)          | 对 x 进行上舍入                                          |
| cos(x)           | 返回 x 的余弦                                            |
| exp(x)           | 返回 Ex 的值                                             |
| floor(x)         | 对 x 进行下舍入                                          |
| log(x)           | 返回 x 的自然对数（底为e）                               |
| max(x,y,z,...,n) | 返回最高值                                               |
| min(x,y,z,...,n) | 返回最低值                                               |
| pow(x,y)         | 返回 x 的 y 次幂                                         |
| random()         | 返回 0 ~ 1 之间的随机数                                  |
| round(x)         | 把 x 四舍五入为最接近的整数                              |
| sin(x)           | 返回 x（x 以角度计）的正弦                               |
| sqrt(x)          | 返回 x 的平方根                                          |
| tan(x)           | 返回角的正切                                             |

### 10、正则表达式

| 修饰符 | 描述                                                     |                                                              |
| :----- | :------------------------------------------------------- | ------------------------------------------------------------ |
| i      | 执行对大小写不敏感的匹配。                               | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_i) |
| g      | 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。 | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_g) |
| m      | 执行多行匹配。                                           |                                                              |



*括号*用于查找一定范围的字符串：

| 表达式 | 描述                       |                                                              |
| :----- | :------------------------- | ------------------------------------------------------------ |
| [abc]  | 查找方括号之间的任何字符。 | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_abc) |
| [0-9]  | 查找任何从 0 至 9 的数字。 | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_0-9) |
| (x\|y) | 查找由 \| 分隔的任何选项。 | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_xy) |

*元字符（Metacharacter）*是拥有特殊含义的字符：

| 元字符 | 描述                                        |                                                              |
| :----- | :------------------------------------------ | ------------------------------------------------------------ |
| \d     | 查找数字。                                  | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_d) |
| \s     | 查找空白字符。                              | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_s) |
| \b     | 匹配单词边界。                              | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_b) |
| \uxxxx | 查找以十六进制数 xxxx 规定的 Unicode 字符。 | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_ux) |

*Quantifiers* 定义量词：

| 量词 | 描述                                |                                                              |
| :--- | :---------------------------------- | ------------------------------------------------------------ |
| n+   | 匹配任何包含至少一个 n 的字符串。   | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_n_1) |
| n*   | 匹配任何包含零个或多个 n 的字符串。 | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_n_2) |
| n?   | 匹配任何包含零个或一个 n 的字符串。 | [试一试](https://www.w3school.com.cn/tiy/t.asp?f=js_regexp_n_3) |

~~~javascript

~~~



