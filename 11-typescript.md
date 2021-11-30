### 1、tsconfig配置文件

1. [配置参照](https://segmentfault.com/a/1190000022809326/)
2. 手动在项目根目录（或其他）创建 tsconfig.json 文件并填写配置；
3. 通过 `tsc --init` 初始化 tsconfig.json 文件。

#### 1.compileOnSave

> `compileOnSave` 属性作用是**设置保存文件的时候自动编译，但需要编译器支持**。

~~~javascript
{
     "compileOnSave": false, //设置保存文件的时候自动编译
}
~~~

#### 2.compilerOptions



> `compilerOptions` 属性作用是**配置编译选项**若 `compilerOptions` 属性被忽略，则编译器会使用默认值，可以查看[《官方完整的编译选项列表》](https://link.segmentfault.com/?enc=8iJ3o9HiQmOwCFPUAA%2FYnw%3D%3D.d%2BqS8OvO8zEmaYLjQQWfcdlaBRmfyXXiO0VWvjhs3PH9W7gZUEE46mqslWNsu9LxnC1D6A%2B8rdibxGCmfBzczvvm1gW7Q9Dn3hOW%2BTDlP64%3D)。编译选项配置非常繁杂，有很多配置，这里只列出常用的配置。

~~~javascript
{
  	"compilerOptions": {
    	"incremental": true, // TS编译器在第一次编译之后会生成一个存储编译信息的文件，第二次编译会在第一次的基础上进行增量编译，可以提高编译的速度
    	"tsBuildInfoFile": "./buildFile", // 增量编译文件的存储位置
    	"diagnostics": true, // 打印诊断信息         (常用)
    	"target": "ES5", // 目标语言的版本            (常用)
    	"module": "CommonJS", // 生成代码的模板标准    (常用)
    	"outFile": "./app.js", // 将多个相互依赖的文件生成一个文件，可以用在AMD模块中，即开启时应设置"module": "AMD",                                  (常用)
    	"lib": ["DOM", "ES2015", "ScriptHost", "ES2019.Array"], // TS需要引用的库，即声明文件，es5 默认引用dom、es5、scripthost,如需要使用es的高级版本特性，通常都需要配置，如es8的数组新特性需要引入"ES2019.Array",
    	"allowJS": true, // 允许编译器编译JS，JSX文件
    	"checkJs": true, // 允许在JS文件中报错，通常与allowJS一起使用
    	"outDir": "./dist", // 指定输出目录          (常用)
    	"rootDir": "./", // 指定输出文件目录(用于输出)，用于控制输出目录结构
    	"declaration": true, // 生成声明文件，开启后会自动生成声明文件
    	"declarationDir": "./file", // 指定生成声明文件存放目录
    	"emitDeclarationOnly": true, // 只生成声明文件，而不会生成js文件
    	"sourceMap": true, // 生成目标文件的sourceMap文件
    	"inlineSourceMap": true, // 生成目标文件的inline SourceMap，inline SourceMap会包含在生成的js文件中
    	"declarationMap": true, // 为声明文件生成sourceMap
    	"typeRoots": [], // 声明文件目录，默认时node_modules/@types
    	"types": [], // 加载的声明文件包
    	"removeComments":true,   //删除注释         (常用)
    	"noEmit": true, // 不输出文件,即编译后不会生成任何js文件
    	"noEmitOnError": true, // 发送错误时不输出任何文件          (常用)
    	"noEmitHelpers": true, // 不生成helper函数，减小体积，需要额外安装，常配合importHelpers一起使用
    	"importHelpers": true, // 通过tslib引入helper函数，文件必须是模块
    	"downlevelIteration": true, // 降级遍历器实现，如果目标源是es3/5，那么遍历器会有降级的实现
    	"strict": true, // 开启所有严格的类型检查                (常用)
    	"alwaysStrict": true, // 在代码中注入'use strict'       (常用)
    	"noImplicitAny": true, // 不允许隐式的any类型           (常用)
    	"strictNullChecks": true, // 不允许把null、undefined赋值给其他类型的变量       (常用)
    	"strictFunctionTypes": true, // 不允许函数参数双向协变
    	"strictPropertyInitialization": true, // 类的实例属性必须初始化
    	"strictBindCallApply": true, // 严格的bind/call/apply检查
    	"noImplicitThis": true, // 不允许this有隐式的any类型               (常用)
    	"noUnusedLocals": true, // 检查只声明、未使用的局部变量(只提示不报错)     (常用)
    	"noUnusedParameters": true, // 检查未使用的函数参数(只提示不报错)
    	"noFallthroughCasesInSwitch": true, // 防止switch语句贯穿(即如果没有break语句后面不会执行)
    	"noImplicitReturns": true, //每个分支都会有返回值
    	"esModuleInterop": true, // 允许export=导出，由import from 导入
    	"allowUmdGlobalAccess": true, // 允许在模块中全局变量的方式访问umd模块
    	"moduleResolution": "node", // 模块解析策略，ts默认用node的解析策略，即相对的方式导入
    	"baseUrl": "./", // 解析非相对模块的基地址，默认是当前目录
    	"paths": { // 路径映射，相对于baseUrl
      // 如使用jq时不想使用默认版本，而需要手动指定版本，可进行如下配置
      	"jquery": ["node_modules/jquery/dist/jquery.min.js"]
    },
    	"rootDirs": ["src","out"], // 将多个目录放在一个虚拟目录下，用于运行时，即编译后引入文件的位置可能发生变化，这也设置可以虚拟src和out在同一个目录下，不用再去改变路径也不会报错
    	"listEmittedFiles": true, // 打印输出文件
    	"listFiles": true// 打印编译的文件(包括引用的声明文件)
  },
     "files":[      // 指定待编译的文件
         "./src/index.ts"
     ]
}
~~~

#### 3. exclude

> `exclude` 属性作用是**指定编译器需要排除的文件或文件夹。**
> 默认排除 `node_modules` 文件夹下文件。

~~~javascript
{
	exclude:[
         "src/lib" // 排除src目录下的lib文件夹下的文件不会编译
    ]
}
~~~

和 `include` 属性一样，支持 glob 通配符：

- `*` 匹配0或多个字符（不包括目录分隔符）
- `?` 匹配一个任意字符（不包括目录分隔符）
- `**/` 递归匹配任意子目录

#### 4. include

> `include` 属性作用是**指定编译需要编译的文件或目录**。

```json
{
    // ...
  "include": [
      //"./src/**/*"
    // "scr" // 会编译src目录下的所有文件，包括子目录
    // "scr/*" // 只会编译scr一级目录下的文件
    "scr/*/*" // 只会编译scr二级目录下的文件
  ]
}
```

#### 5.files

> `files` 属性作用是**指定需要编译的单个文件列表**。
> 默认包含当前目录和子目录下所有 TypeScript 文件。

```json
{
    // ...
  "files": [
    // 指定编译文件是src目录下的leo.ts文件
    "scr/leo.ts"
  ]
}
```

#### 6. extends

> `extends` 属性作用是**引入其他配置文件，继承配置**。
> 默认包含当前目录和子目录下所有 TypeScript 文件。

~~~json
{
    // ...
  // 把基础配置抽离成tsconfig.base.json文件，然后引入
    "extends": "./tsconfig.base.json"
}
~~~

#### 7. references

> `references` 属性作用是**指定工程引用依赖。**
> 在项目开发中，有时候我们为了方便将前端项目和后端`node`项目放在同一个目录下开发，两个项目依赖同一个配置文件和通用文件，但我们希望前后端项目进行灵活的分别打包，那么我们可以进行如下配置：

```json
{
    // ...
  "references": [ // 指定依赖的工程
     {"path": "./common"}
  ]
}
```

#### 8. typeAcquisition

`typeAcquisition` 属性作用是**设置自动引入库类型定义文件(.d.ts)相关。**
包含 3 个子属性：

- `enable` : 布尔类型，是否开启自动引入库类型定义文件(.d.ts)，默认为 false；
- `include` : 数组类型，允许自动引入的库名，如：["jquery", "lodash"]；
- `exculde` : 数组类型，排除的库名。

```json
{
    // ...
  "typeAcquisition": {
    "enable": false,
    "exclude": ["jquery"],
    "include": ["jest"]
  }
}
```

### 2、基本类型

~~~typescript
// 1.number 任意数值     声明和赋值同时进行  -> 自动检测类型
let num:number = 123;
let num1:number;
num1 = 234

// 2.string 任意字符串
let str:string;
str = '字符串';
let str:string = '字符串';

// 3.boolean  false | true
let b:boolean;
b = true;
let b2:boolean = false;

// 4.字面量
let data:'str' | 123
data = 'str';
data = 123

// 5.any 任意类型
let ay: any   //关闭检测   -> 任意类型

// 6.unknown 类型安全的any    只能将 unknown 类型的变量赋值给 any 和 unknown。  
function Type(callback:unknown){         //强制执行类型检查
	if(typeof callback === 'function'){
		callback()
    }
}

// 7.void 空值(undefined  null)
function fun():void{
	console.log('没有返回值')
}
let aa: void;
aa = null;

// 8.never 没有值
function fn2(): never {
    throw new Error('报错了')
}

// 9.object 任意对象
let ao: object
ao = { name: 'xiaohong', age: 55 }       //任意个数
let ao1: { name: string, age: number } = { name: 'ahha', age: 123 }    //指定个数
let ao2: { name: string, age?: number }     //表示可选参数
let ao3: { name: string, [propName: string]: string }    //任意属性名 值为字符串
ao3 = { name:'', age: '55' }

// 10.array 任意数组
let ar: Array<string>      let ar2: string[]  // 第二中写法
ar = ['仅支持字符串']
let ar1: Array<number>
ar1 = [1, 2, 3]

// 11.元组 tuple
let ar3: [string, number] //必须满足类型 且数组个数相同
ar3 = ['string',2];

// 12.enum 枚举
enum Gender {male,Female = 3}
console.log(Gender.male,Gender.Female)  // 打印 0 和 3

// 注意:
let J = {name:string} & {age:number} // 同时满足两个
// 使用type 关键字定义类型别名 
type mathType = string | number
let math: mathType;
math = '只能赋值为字符串和数字'
~~~

### 3、函数的使用

~~~typescript
let fun:(a:number,b:number) => number   //参数指定类型和返回的类型
let fun: (a: number, b: number) => string
fun = function (a: number, b: number) {
    return a + b + ''
}

let func1(a:number,b:number):string{     // 若函数没有返回值 则使用 :void
    return a + b +''
}
~~~

### 4、类的定义

~~~typescript
class Person {
    name: string    //此处省略了public 关键字
    age: number
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    run(): void {
        console.log('正在奔跑');
    }
    getName(name: string): void {
        this.name = name
    }
}
~~~

### 5、接口的使用

~~~typescript
function printLabel(info:{label:string}) //参数必须是一个对象 并且数字属性为字符串

//使用interface 定义接口
interface fullName{
    fristName:string;
    secondName:string;
    age?:number
}
function test(params:fullName){}

//加密函数类型接口
interface encrypt{
	(key:string,value:string):string
}
let md5:encrypt = function(key:string,value:string):string{}

//可索引接口
interface UserArr {
    [index: number]: string
}
let testarr: UserArr = ["1", "5"]

interface UserObj {
    [index: number]: number
}
let testobj: UserObj = {
    5: 4
}
~~~



~~~typescript
//类接口 (满足接口)
interface Animal {
    name: string;
    eat(str: string): void
}

class Dog implements Animal {
    name: string
    constructor(name: string) {
        this.name = name
    }
    eat() {
        console.log(this.name);
    }
}
//接口继承
interface Animal {
    eat(): void;
}
interface dog {
    name: string;
}

class Dog implements Animal {
    name: string
    constructor(name: string) {
        this.name = name
    }
    eat() {
        console.log('小狗在奔跑');
    }
}
~~~

### 6、泛型

~~~typescript
function test<T>(a:T):T{
    return a
}
test<number>(99)

//泛型类
class Min<T>{
	list:T[] = []
    add(value:T):void{
		this.list.push(value)
    }
    min():T{
		let min = this.list[0];
        for(var i =0;i< this.list.length; i++){
			if(min > this.list[i]){
				min = this.list[i]
            }
        }
        return min
    }
}
let m  = new Min<string>();
m.add('a');
m.add('h');
m.min() //a

//函数泛型接口
interface ConfigFn {
    <T>(value: T): T
}
const test1: ConfigFn = function <T>(value: T): T {
    return value
}
//第二种方法
interface ConfigFn1<T> {
    (value: T): T
}
function test2<T>(value: T): T {
    return value
}
let myMethod: ConfigFn1<string> = test2
test2('字符串')
~~~

