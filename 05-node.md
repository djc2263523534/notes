### Node.js

### 1.学习链接导航

+ javaScript 标准参考教程(alpha) :  [http://javascript.ruanyifeng.com/]()
+ Node 入门 ：[https://www.nodebeginner.org/index-zh-cn#about]()
+ 深入浅出Node: https://www.infoq.cn/article/nodejs-module-mechanism
+ CNODE社区：[https://cnodejs.org/]()
  + CNODE-新手入门：[https://cnodejs.org/ge												tstart]()
+ Content-Type:  [https://tool.oschina.net/commons]()
+ Mongodb: https://www.runoob.com/mongodb/mongodb-connections.html
+ https://lurongtao.gitee.io/felixbooks-gp19-node.js/basics/04-Koa2.html
+ 框架：https://www.bootcdn.cn/
+ cookie: https://www.cnblogs.com/loaderman/p/11506682.html

1. cors 跨域请求

2. fastclick   200ms点击延迟

3. npm i postcss-px-to-viewport --save-dev

4. npm install better-scroll -S 

   

### 1.初识Node

1. EcmaScript
2. 文件读写
3. 网络服务器的构建
4. 网络通信
5. http 服务器的部署
6. event-driven 事件驱动
7. non-blocking I/O model 非阻塞IO模型(异步)
8. lightweight and efficient 轻量和高效

+ B/S 编程模型
  + Browser-Server
  + back-end
  + 任何服务端技术这种 BS 编程模型都是一样，和语言无关
  + Node 只是作为我们学习BS编程模型的一个工具

+ 模块化编程
  + RequireJS
  + seaJS
  + `@import('文件路径')`
  + 以前认知的JavaScript 只能通过 `script` 标签来加载
  + 在Node 中可以象 `@import('文件路径')` 一样来引用来加载Javasript脚本文件

+ Node常用的API
+ 异步编程
  + 回调函数
  + Promise
  + async
  + generator

+ Express Web 开发框架
+ Ecmascript 6语法

### 2.核心模块

url, querystring, http, events, fs, stream, readline, crypto, zlib

1. fs 文件系统模块(file system)
2. http 服务器模块
3. url 路径操作模块
4. path 路径处理模块
5. os 操作系统信息模块
6. art-template 第三方模块

+ CommonJS模块化
  + 模块作用域
  + 使用 `require` 方法用来加载模块
  + 使用 `exports ` 接口对象来导出模块中的成员

### 2.文件读写

~~~javascript
//1.引入模块
var fs = require('fs');

//2. 读取文件
//  第一个参数就是要读取文件的路径
//  第二个参数就是一个回调函数
//    成功 
//      data 数据
//      error null
//    失败
//      data null
//      error 错误对象
fs.readFile('./data/hellow.txt', function (error, data) {
    console.log(data.toString());
    console.log(error);
    if (!error) {
        console.log('文件读取成功');
    }res.header("Content-Type","text/plain;charset=utf-8")
})

//3.写入文件
fs.writeFile('./data/你好.md', '大家好介绍一下自己', function (error) {
    console.log('文件写入成功');
})

//4.读取文件路径
fs.readdir('./Apache', (err, data) => {
    if (!err) {
        console.log(data);
    }
})
//5.追加内容
fs.appendFile("test.txt", "人间失格", 'utf-8', function(err) {
    if(err) {
        console.log(err);
        return false;
    }
    console.log('写入成功!!!');
});

//6.写入流文件
const fs = require('fs');
let ws = fs.createWriteStream('hellow.txt', { flags: 'w', encoding: 'utf-8' })

ws.on('open', () => {
    console.log('文件打开了');
})

ws.on('ready', () => {
    console.log('文件写入已准备');
})

ws.on('close', () => {
    console.log('写入完成');
})
ws.write('hellow world呵呵', (err) => {
    if (err) {
        console.log(err);
    } else {
        console.log('写入成功');
    }
})
ws.write('黑恶黑', (err) => {
    if (err) {
        console.log(err);
    } else {
        console.log('写入成功');
    }
})
ws.end()

//7.读取流并写入
et rs = fs.createReadStream('./music/About_航大 - 风的颜色 (原唱_ 乃万).mp3')
let ws = fs.createWriteStream('a.mp3')

rs.on('open', () => {
    console.log('读取流打开了');
})

rs.on('close', () => {
    ws.end()
    console.log('读取流关闭了');
})

rs.on('data', (chunk) => {
    console.log('单批流入:' + chunk.length);
    console.log(chunk);
    ws.write(chunk, () => {
        console.log('单批写入成功');
    })
})
//方法二
let rs = fs.createReadStream('./music/About_航大 - 风的颜色 (原唱_ 乃万).mp3')
let ws = fs.createWriteStream('b.mp3')

rs.on('open', () => {
    console.log('读取流打开了');
})

rs.on('close', () => {
    ws.end()
    console.log('读取流关闭了');
})

rs.pipe(ws)
~~~

### 7.创建Web服务器

~~~javascript
//1.加载 http 核心模块
var http = require('http');

//2.使用 http.createServer() 方法创建一个web 服务器

var server = http.createServer();

//3.服务器要干嘛
//   提供服务 ：对接数据
//   发送请求
//   接受请求
//   处理请求
//   响应
// request 请求事件处理函数 ，需要两个参数
//      Request 请求对象
//        请求对象可以用来获取客户端的一些请求 
//      Respone 响应对象

//监听服务器事件
server.on('request', function (request, respone) {
    // http://127.0.0.1:300/
    console.log('收到请求了' + request.url);
    
    if (request.url == '/products') {
        var products = [
            {
                name: '小米1',
                price: 1157
            },
            {
                name: '小米2',
                price: 1157
            }
        ]
        respone.end(JSON.stringify(products))
    }

    if (request.url == '/') {
        respone.end('index page')
    } else if (request.url == '/login') {
        respone.end('login page')
    } else {
        respone.end('404 Not Found')
    }

})
})
/* 
    请求不同的路径的时候响应不同的结果
    例如：
        /index
        /login 登录
        /register 注册
        / hahha 哈哈哈
*/

// 4.绑定端口号 ，启动服务器
server.listen(3000, function () {
    console.log('服务启动成功了，可以通过 http://127.0.0.1:300/来进行访问');
})
~~~

+ ip地址和端口号
  + ip地址用来定位计算机
  + 端口号用来定位具体的应用程序
  + 一切需要联网通信的软件都会占用一个端口号
  + 端口号的范围从0-65536之间
  + 在计算机中有一些默认端口号，最好不要去使用  例如 http 服务的80
  + 开发过程中使用一些简单好记的就可以了 例如 ：3000  5000  等没什么含义的

### 8.art-templat的初识

~~~html
	<script type="text/template" id="tp1">
        大家好，我叫：{{name}}
        我今年{{age}} 岁了
        我来自{{from}}
        我喜欢{{each hobby}}{{$value}}{{/each}}
    </script>
    <script>
        var ret = template('tp1', {
            name: 'Jack',
            age: 18,
            from: '江西',
            hobby: ['听音乐、', '看电视、', '打篮球']
        })
        console.log(ret);
    </script>

2.{{include '路径'}}
3.继承
<!-- 留一个坑 -->
    {{block "content"}}
    <h2>默认内容</h2>
    {{/block}}
<!-- 引入并填坑替换 -->
{{extend './list.html'}}
{{block 'content'}}
<h2>index 页面被替换了</h2>
{{/block}}
~~~

### 9.服务端渲染

~~~javascript
const fs = require('fs');
const http = require('http')
const template = require('art-template')

const server = http.createServer()
server.on('request', (req, res) => {
    let url = req.url
    //1.读取文件
    fs.readFile('./Apache/art-template-Ap.html', (err, data) => {

        if (!err) {
            //2.读取文件路径
            fs.readdir('./Apache', (err, files) => {

                //3.将模板字符读取后 转化为字符串 通过 render 方法解析模板
                if (!err) {
                    var html = template.render(data.toString(), {
                        title: '主页',
                        files: files
                    })
                    res.end(html)
                }
            })
        }
    })
})
server.listen(3000, () => {
    console.log('server is runing ...');
})
~~~

### 10.静态资源

1. http://127.0.0.1:3000/+ 引入文件的路径发送请求资         例如：http://127.0.0.1:3000/index.css
2. url.parse("http://127.0.0.1:3000/post?name=1121&text=4",true(可选参数))  解析请求路径中的查询字符串 

~~~javascript
/* 
    在浏览器收到 html 响应之后 ，就要开始从上到下依次解析
    当在解析的过程中 ，如果发现  link img  iframe  video audio 资源会下向服务器自动发出请求
       
	为了让目录结构保持统一清晰 所以我们约定， 把所有的HTML 文件都放到 views 
	我们为了方便的统一处理这些静态资源 所有我们约定把所有的静态资源都存放在 public 目录
        public 目录中的资源都允许被访问
*/
var http = require('http');
var fs = require('fs')
var template = require('art-template');
var url = require('url');
var comments = [
    {
        name: '张三',
        message: '今天天气真不错',
        dateTime: '2020年'
    },
    {
        name: '张三',
        message: '今天天气真不错',
        dateTime: '2020年'
    }
]
http.createServer((req, res) => {
    var parseObj = url.parse(req.url, true)
    let pathname = parseObj.pathname
    if (pathname == '/') {
        fs.readFile('./views/template-index.html', (err, data) => {
            if (!err) {
                var html = template.render(data.toString(), {
                    comments: comments
                })
                res.end(html)
            } else {
                res.end('404 Not Found')
            }
        })

        //http://127.0.0.1:3000 /public/css/main.css
    } else if (pathname == '/post') {
        fs.readFile('./views/post.html', (err, data) => {
            if (!err) {
                res.end(data)
            } 
        })
    } else if (pathname == 'pinlun') {
        var comment = parseObj.query
        comment.dateTime = '2020'
        comments.push(comment)
        /* 
            让服务器进行重定向
                1.状态码设置 302 临时重定向   301 永久重定向
                2.在响应头中通过 Location 告诉客户端往哪重定向
                如果客户端受到服务器的响应的状态码是302 就会自动去响应头中找 Lacation 
            所以你就能看到客户端自动跳转了
        */
        res.statusCode = 302
        res.setHeader('Location', '/')
        res.end()

    }
    else if (pathname.indexOf('/public/') === 0) {  
        /* 重点：
        	   /public/css/main.css
         	   /public/js.main.js
           当需要加载的某些资源时，浏览器向服务端自动发送请求，通过public 文件加将静态资源公开
        */
        fs.readFile('.' + pathname, (err, data) => {
            if (!err) {
                res.end(data)
            }
        })
    } else {
        fs.readFile('./views/404.html', (err, data) => {
            if (!err) {
                res.end(data)
            }
        })
    }

}).listen(3000, () => {
    console.log('server is runing ....');
})
~~~

### 11.模块系统

1. 导出 ：`exports`  `module.exports`   
2. 导入：`require`
3. `exports ==  module.exports`

~~~javascript
// 1.exports导出单个成员 对象中的每个成员
    exports.foo = 'hellow'
	exports.a = function(){
        console.log()
    }
	exports.d ={
		foo:'helllow'
    }
//2.module.exports 导出拿到的对象 
module.exports = 'hellow'
~~~

~~~javascript
//3.以下情况将会覆盖
module.exports = 'hellow'

module.exports = function(x,y){
    return x+y
}

//4.也可以直接导入一个对象
module.exports ={}
~~~

### 12.npm

1. node package manager              npm init  (npm init --y[yes])   
2. **-S, --save 安装包信息将加入到dependencies（生产阶段的依赖）**
3. **-D, --save-dev 安装包信息将加入到devDependencies（开发阶段的依赖），所以开发阶段一般使用它**
4. **-O, --save-optional 安装包信息将加入到optionalDependencies（可选阶段的依赖** 

~~~javascript
1.npm install 包名 --registry=https://registry.npm.taobao.org
npm install 安装模块
npm uninstall 卸载模块
npm update 更新模块
npm outdated 检查模块是否已经过时
npm ls 查看安装的模块
npm init 在项目中引导创建一个package.json文件
npm help 查看某条命令的详细帮助
npm root 查看包的安装路径
npm version 查看模块版本
npm view 查看模块的注册信息
3.1.1 查看当前源
npm config get registry
3.1.2 切换淘宝源
npm config set registry https://registry.npm.taobao.org
~~~

### 13.Express

1. 创建服务器

~~~javascript
//1.使用express创建本地服务器
const express = require('express');

const app = express()  //启用本地服务器

app.get('/', (req, res) => {
    res.end('hellow world')
})

app.listen(3000, () => {
    console.log('runing ....');
})
~~~

2. 公开静态资源

~~~java
1.app.use(express.static('public'))  
    现在，你就可以访问 public 目录中的所有文件了
    http://localhost:3000/images/kitten.jpg
	http://localhost:3000/css/style.css
	http://localhost:3000/js/app.js

2.app.use('/static', express.static('public'))
	http://localhost:3000/static/images/kitten.jpg
	http://localhost:3000/static/css/style.css
	http://localhost:3000/static/js/app.js
~~~

3. 修改完代码自动重启

nodemon 是基于 Node 开发的第一个第三方命令行工具 

~~~javascript
npm install --g nodemon
nodemon app.js  
//只要通过 nodemon 启动的服务，则它会监视你的文件变化 当文件发生变化的时候 自动帮你重启服务器
~~~

### 14.基本路由

1. Express 中配置 `art-template` 模板引擎

~~~javascript
//1.安装
npm install --save art-template 
npm install --save express-art-template

//2.使用
var express = require ( 'express' ); 
var app = express();

// 查看引擎设置 express 和 art-template
app.engine( 'html' , require ( 'express-art-template' )); 
//设置路径
app.set( 'views' , path.join(__dirname, 'views' ) 修改后的路径); 

// 路由
app.get( '/' , function ( req, res ) { 
    //express 默认会去项目中的views 目录中找 index.art
    res.render( 'index.html' , { 
        user: { 
            name: 'aui' , 
            tags: [ 'art' , 'template' , ' nodejs' ] 
        } 
    }); 
})
~~~

2. 在 Express 获取表单 POST 请求数据

~~~javascript
//1.安装模块
$ npm install body-parser

// 2.使用body-parser
var express = require('express')
var bodyParser = require('body-parser')
var app = express()

//3.配置body-parser  属性req.body 获取表单传过来的
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

app.get('/', (req, res) => {
    res.render('index.html', {
        comments: comments
    })
})
app.get('/post', (req, res) => {
    res.render('post.html')
})

app.post('/post', (req, res) => {
    let comment = req.body;
    comment.dateTime = '2021'
    comments.unshift(comment)
    res.redirect('/')
})
~~~

### 15.配置路由

1. 导出 router

~~~javascript
const express = require('express')
const fs = require('fs');

//1.创建一个路由容器
const router = express.Router()

//2.把路由都挂在到路由容器中
router.get('/', (req, res) => {
    fs.readFile('./db.json', 'utf8', (err, data) => {
        /*  
            将读取的数据转换为 utf8 字符串
            把字符串解析为对象
        */
        let obj = JSON.parse(data)
        if (!err) {
            res.render('index.html', {
                fruits: obj.fruits,
                students: obj.students,
            })
        } else {
            res.status(500).end('Server err')
        }
    })
})
router.get('/students/new', (req, res) => {
})

})

//3.把 router 路由导出
module.exports = router
~~~

2. 导入并使用 router

~~~javascript
const express = require('express');
var bodyParser = require('body-parser')

const router = require('./router')  //把路由导入

//开启服务器
const app = express()
// 公开静态资源
app.use('/static', express.static('./public/'))
//配置 express 和 art-template
app.engine('html', require('express-art-template'));

//配置post 请求
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

//路由容器的所有路由挂在到 app 服务中
app.use(router)

app.listen(3000, () => {
    console.log('runing...');
})
~~~

~~~javascript
//path 路径模块
path.basename(path[, ext])  文件名
path.extname(path)  文件扩展名
path.isAbsolute(path) 是否为绝对路径
path.join([...paths])    路径拼接
path.parse(path)      路径转化为对象

path.dirname(path)    文件目录路径
path.filename(path)    文件路径
~~~

#### 1、响应方法

下表中响应对象（res）的方法向客户端返回响应，终结请求响应的循环。如果在路由句柄中一个方法也不调用，来自客户端的请求会一直挂起。

| 方法             | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| res.download()   | 提示下载文件。                                               |
| res.end()        | 终结响应处理流程。                                           |
| res.json()       | 发送一个 JSON 格式的响应。                                   |
| res.jsonp()      | 发送一个支持 JSONP 的 JSON 格式的响应。                      |
| res.redirect()   | 重定向请求。                                                 |
| res.render()     | 渲染视图模板。                                               |
| res.send()       | 发送各种类型的响应。                                         |
| res.sendFile     | 以八位字节流的形式发送文件。                                 |
| res.sendStatus() | 设置响应状态代码，并将其以字符串形式作为响应体的一部分发送。 |

