### 1、创建项目

1. 创建一个项目 `vue create 项目名称`
2. 使用图形化界面管理 `vue ui`

~~~markdown
? Check the features needed for your project: (Press to select, to toggle all, to invert selection)
( ) Babel               //转码器，可以将ES6代码转为ES5代码，从而在现有环境执行。
( ) TypeScript// TypeScript是一个JavaScript（后缀.js）的超集（后缀.ts）包含并扩展了 JavaScript 的语法，需要被编译输出为 JavaScript在浏览器运行，目前较少人再用
( ) Progressive Web App (PWA) Support        // 渐进式Web应用程序
( ) Router                                   // vue-router（vue路由）
( ) Vuex                                     // vuex（vue的状态管理模式）
( ) CSS Pre-processors                       // CSS 预处理器（如：less、sass）
( ) Linter / Formatter                       // 代码风格检查和格式化（如：ESlint）
( ) Unit Testing                            // 单元测试（unit tests）
( ) E2E Testing                             // e2e（end to end） 测试
~~~

~~~markdown
module.exports = {
  baseUrl: '/',// 部署应用时的根路径(默认'/'),也可用相对路径(存在使用限制)
  outputDir: 'dist',// 运行时生成的生产环境构建文件的目录(默认''dist''，构建之前会被清除)
  assetsDir: '',//放置生成的静态资源(s、css、img、fonts)的(相对于 outputDir 的)目录(默认'')
  indexPath: 'index.html',//指定生成的 index.html 的输出路径(相对于 outputDir)也可以是一个绝对路径。
  pages: {//pages 里配置的路径和文件名在你的文档目录必须存在 否则启动服务会报错
    index: {//除了 entry 之外都是可选的
      entry: 'src/index/main.js',// page 的入口,每个“page”应该有一个对应的 JavaScript 入口文件
      template: 'public/index.html',// 模板来源
      filename: 'index.html',// 在 dist/index.html 的输出
      title: 'Index Page',// 当使用 title 选项时,在 template 中使用：<title><%= htmlWebpackPlugin.options.title %></title>
      chunks: ['chunk-vendors', 'chunk-common', 'index'] // 在这个页面中包含的块，默认情况下会包含,提取出来的通用 chunk 和 vendor chunk
    },
    subpage: 'src/subpage/main.js'//官方解释：当使用只有入口的字符串格式时,模板会被推导为'public/subpage.html',若找不到就回退到'public/index.html',输出文件名会被推导为'subpage.html'
  },
  lintOnSave: true,// 是否在保存的时候检查
  productionSourceMap: true,// 生产环境是否生成 sourceMap 文件
  css: {
    extract: true,// 是否使用css分离插件 ExtractTextPlugin
    sourceMap: false,// 开启 CSS source maps
    loaderOptions: {},// css预设器配置项
    modules: false// 启用 CSS modules for all css / pre-processor files.
  },
  devServer: {// 环境配置
    host: 'localhost',
    port: 8080,
    https: false,
    hotOnly: false,
    open: true, //配置自动启动浏览器
    proxy: {// 配置多个代理(配置一个 proxy: 'http://localhost:4000' )
      '/api': {
        target: '<url>',
        ws: true,
        changeOrigin: true
      },
      '/foo': {
        target: '<other_url>'
      }
    }
  },
  pluginOptions: {// 第三方插件配置
    // ...
  }
};
~~~

### 2、vue配置别名

~~~javascript
module.exports = {
    configureWebpack: {
        resolve: {
            alias: {
                // '@' 是 './src' 的别名，vue-cli 默认配置
                'assets': '@/assets',
                'components': '@/components',
                'network': '@/network',
                'views': '@/views',
                'common': '@/common'
            }
        }
    }
}
~~~

### 3、指令

1. 内容渲染指令

   - v-text   渲染标签内容 (不解析标签会显示为<h1>hello wold</h1>)
   - v-html   解析html标签
   - {{}}    插值语法

2. 属性绑定

   - v-bind     简写=>    :

3. 条件判断

   - v-if               控制模板里元素的显示和隐藏，值为true就显示，为false就隐藏
   - v-if else      配合使用
   - v-else-if      可以实现多分支逻辑
   - v--show    只是简单地切换元素的 CSS 属性 display

4. 不常用指令

   - v-cloak         当元素上加上v-cloak指令的时候，在vue没有加载的时候，
     这个指令就相当于p标签的一个标签属性，当vue加载完成后，会将这个指令去掉
     依靠这个属性可以实现防止{{}}闪烁

5. 事件指令

   - v-on    简写 =>    @      后面加上要绑定的事件类型      默认会在方法中传入事件对象 ($event)

     修饰符 ：

     ​			.prevent  阻止默认事件                                     .shop  阻止冒泡

     ​			.enter 敲回车事件    event.keycode		   	.native	组件添加事件 

6. 双向绑定

   - v-model     只允许在表单中使用

     修饰符：

     ​			.lazy - 监听 change 而不是 input 事件            .number - 输入字符串转为有效的数字

     ​			.trim - 输入首尾空格过滤

7. 列表循环

   - 数组 :   v-for="(item,index,arr) in array" :key="index"
   - 对象 ：v-for="(value,key,index) in object " :key="index"

### 4、过滤器(vue2)

1. 私有过滤器(就近原则)

~~~vue
<p>过滤器的使用 {{100 | math | xxx(多次过滤)}}</p>

定义：
filters:{
	math(value){
		return value / 10
	}
}

//全局过滤器
Vue.filters(math,(value)=> {
	return value + "拼接一个字符串"
})
~~~

### 5、监听器

~~~vue
data(){
	return {
		message:'简单监听器的用法',
		userInfo:{
			user："admin"
		}    
	}
}
watch:{
方法一： 方法格式的监听器
	message(newValue,oldValue){
		newvalue => 被改变后的值
		oldvalue => 未改变的值
	},
方法二： 对象格式的监听器
	message：{   
		handler(){
			监听器处理函数
		}，
		immediate:true  (一进入就触发)
	},
方法三：深度监听(对象属性)
	userInfo:{
		复杂用法
		handler(){
		
		},
		deep:true  (深度监听)
	}
		建议使用
		'userInfo.user'(){
			
	}

}
~~~

> 

### 7、样式冲突

1. scope  组件作用域
2. /deep/  样式穿透



### 10、获取Dom元素

1. 

### 11、动态组件

1. 使用component的 is属性(:is 动态渲染)
2. include   缓存组件      exclude  没有缓存的组件

​	

~~~vue
<keep-link include="组件名">
	<component :is=""></component>        	动态组件的使用
</keep-link>
~~~

### 12、插槽的使用

1. 基本使用
2. 具名插槽  name="default" (默认名称)     简写：#default
3. 作用域插槽   <slot msg='数据'></slot>

~~~vue
1.封装组件(父组件)<fater>
<slot name="child1"></slot>
<slot name="chlid2" msg='作用域插槽传递数据'></slot>

2.使用组件
 <fater>
     <template v-slot:child1></template>
 </fater>

3.作用域插槽的使用
  <fater>
  	<template #child2="scope"></template>  可以通过结构赋值来获取数据
  </fater>
~~~

### 12、自定义指令

![Snipaste_2021-10-22_19-18-46](C:\Users\坟场蹦迪\Desktop\工具箱\笔记\image\Snipaste_2021-10-22_19-18-46.png)

~~~vue
1.私有自定义指令          v-color="'red'"
directives:{
	color:{
		bind(el,binding){   //只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置
			//形参中的el 是绑定了此指令的 原生的DOM 对象
			1.el.style.color = 'pink'             
			2.el.style.color = binding.value
		},
		inserted(){
			//被绑定元素插入父节点时调用
		}        
	 	updata(el,binding){
			//所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前
			el.style.color= binding.value
		},
		componentUpdated(){
			//指令所在组件的 VNode 及其子 VNode 全部更新后调用
		},
		unbind(){}
	    	//只调用一次，指令与元素解绑时调用
		}
}
简写方法：
directives:{
	color(el,binding){
		el.style.color = binding.value
	}
}

2.全局自定义指令(简写)
Vue.directives('color',(el,bindind) => {
	el.style.color = binding.value
})
~~~

### 13、render函数的使用

1. 返回一个createElement( **标签名** ,  **Object** ,  **Array**)接收三个参数(删除template)

~~~javascript
render(createElement) {
    // return createElement("h2", "哈哈");
    return createElement(      // 标签名 -> 对象 -> 数组
      "div",
      {
        // class: "xxclass",
        style: { color: "red" },
        // domProps: { innerHTML: "哈哈" },
        attrs: { id: "xxid", class: "hh" },
      },
      [
        createElement("h1", "11"),
        createElement("h2", "22"),
        createElement("h3", {
          class: "xx1",
          domProps: {
            innerHTML: "999",
          },
        }),
      ]
    );
  },
~~~

### 14、Mixins的使用

1. 数据对象在内部会进行递归合并，并在发生冲突时以**组件数据优先**
2. 同名钩子函数将合并为一个数组，因此都将被调用。另外，**混入对象的钩子将在组件自身钩子之前调用**
3. 值为对象的选项，例如 `methods`、`components` 和 `directives`，将被合并为同一个对象。两个对象键名冲突时，**取组件对象的键值对**

~~~javascript
export const myMixin = {
    data(){   
		message:'数据'
    },
    create(){
		console.log('我是混入的钩子')
    }，
    methods:{
		sameFn(){
			console.log('名字相同是自身组件优先')
        }
	}
}
//全局混入一般不使用
Vue.mixin({
  created() {
    console.log('我是全局的钩子');
  }
})

//使用
import myMixin from 'Mixin';
mixins:[myMixin]
~~~



~~~javascript
 $route: {
      handler: function (route) {
        this.redirect = route.query && route.query.redirect;
      },
      immediate: true,
    },
~~~

### :star:组件通信

### 1、父传子(值)

~~~vue
1.父组件
<children path="home"></children>
~~~

~~~vue
2.子组件
props:{ 
	one:String,
	two:[String,Array],
	// 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
}
props:["path"],  //不指定类型
props:{
	prop1:{
		type: 数据类型，
		default: 默认值，  (如果是一个对象 则必须是一个方法)
		required: true (必须传值)
	}
}
~~~

~~~javascript
//$attrs $listeners   v-bind="$attrs"      v-on="$listeners"
~~~

> $attrs  包含了父作用域中不作为 prop 被识别 (且获取) 的 attribute 绑定 (`class` 和 `style` 除外)。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 (`class` 和 `style` 除外)，并且可以通过 `v-bind="$attrs"` 传入内部组件——在创建高级别的组件时非常有用

### 2、自定义事件

1. 子组件发射事件    this.$emit(事件名 , 参数)
2. 父组件接收

~~~vue
1.子组件
<button @click="children">发射事件</button>
methods:{
	children(){
		this.$emit('child',参数)
	}
}
2.父组件
<children @child="btnClick"></children>
methods:{
	btnClick(参数){}
}
~~~

### 3、数据共享

![数据共享](C:\Users\坟场蹦迪\Desktop\工具箱\笔记\image\数据共享.png)

~~~vue
1.兄弟组件数据共享
import  mitt  from 'mitt'
const bus = mitt()

export default bus
bus.emit() bus.on()
~~~

### 4、注入依赖

> 这种方式就是Vue中的**依赖注入**，该方法用于**父子组件之间的通信**。当然这里所说的父子不一定是真正的父子，也可以是祖孙组件，在层数很深的情况下，可以使用这种方法来进行传值。就不用一层一层的传递了

> **注意：** 依赖注入所提供的属性是**非响应式**的

~~~javascript
//父组件
provide(){
	return {
        message:'我是注入的数据'
    }
}
~~~

~~~javascript
//子组件
inject:["message"]
inject:{
	message:{
        from：message     //property 是在可用的注入内容中搜索用的 key (字符串或 Symbol)
		default          //property 是降级情况下使用的 value (值)
    }
}   注意：message为接收的名字 from指定来源(有可能来自父级多代....祖)
~~~

### 5、组件实例

1. 定义  ref="name"
2. 获取ref 对象      this.$refs['name']     =>  可以使用 子组件内的方法
3. this.$nextTick(() => {  当数据发生发生变化的时候  在Dom 还没有渲染的时候是那不到 ref 的})       

### 6、父子组件

- 使用`$parent`可以让组件访问父组件的实例（访问的是上一级父组件的属性和方法）
- 使用`$children`可以让组件访问子组件的实例，但是，`$children`并不能保证顺序，**并且访问的数据也不是响应式的**。

###  :star:VueRouter

### 1、路由的使用

1. $router  跳转和传参
2. $route    获取参数

~~~vue
inport Vue from 'vue'
inport VueRouter from 'vue-router'

const routes = {
  path: string,     路径名
  component?: Component,    渲染的模板
  name?: string, // 命名路由
  components?: { [name: string]: Component }, // 命名视图组件
  redirect?: string | Location | Function,     //重定向
  props?: boolean | Object | Function,        //路由传参
  alias?: string | Array<string>,       //url 保持别名
  children?: Array<RouteConfig>, 				// 嵌套路由
  beforeEnter?: (to: Route, from: Route, next: Function) => void,
  meta?: any,

  // 2.6.0+
  caseSensitive?: boolean, // 匹配规则是否大小写敏感？(默认值：false)
  pathToRegexpOptions?: Object // 编译正则的选项
}



const router = new VueRouter({
	 mode: 'history',     //hash
  	 base: process.env.BASE_URL,
  	 routes,
     linkActiveClass: '类名'  //设置激活的class

})

router.beforeEach((to, form, next) => {
  //如果用户访问的路径是登录页，直接放行
  if (to.path === '/login') return next()
  //获取保存的 seccionStorage 值
  const tokenStr = sessionStorage.getItem('token')
  //没有token 强制跳转登录页
  if (!tokenStr) return next('/login')
  next()

})
      
      
~~~

###  2、路由的跳转

~~~vue
<!-- 字符串 -->
<router-link to="home">Home</router-link>
<!-- 渲染结果 -->
<a href="home">Home</a>

<!-- 使用 v-bind 的 JS 表达式 -->
<router-link v-bind:to="'home'">Home</router-link>

<!-- 不写 v-bind 也可以，就像绑定别的属性一样 -->
<router-link :to="'home'">Home</router-link>

<!-- 同上 -->
<router-link :to="{ path: 'home' }">Home</router-link>

<!-- 命名的路由 -->
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>

<!-- 带查询参数，下面的结果为 /register?plan=private -->
<router-link :to="{ path: 'register', query: { plan: 'private' }}">Register</router-link>


replace     导航后不会留下 history 记录          active-class  设置链接激活时使用的 CSS 类名(可配置)
append       当前 (相对) 路径前添加基路径		  exact    链接使用“精确匹配模式
tag			渲染成某种标签
~~~

###  :star:axios

### 1、安装



```
$ npm install axios

在 vue 中全局挂载
Vue.prototype.$axios = axios

```

~~~javascript
// 发送 POST 请求
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});

// 获取远端图片
axios({
  method:'get',
  url:'http://bit.ly/2mTM3nY',
  responseType:'stream'
})
  .then(function(response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
});
~~~

### 2、Get方法

1. axios.get(url,{ params:{}})      返回一个Promise

~~~javascript
 1.为给定 ID 的 user 创建请求
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

2.上面的请求也可以这样做
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
~~~

### 3、Post方法

1. axios.post(url, 参数对象)

~~~javascript
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
~~~

### 4、多个请求

1. axios.all()

~~~javascript
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // 两个请求现在都执行完成
  }));
~~~

### 5、实例创建

~~~javascript
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});

instance({}).then()
~~~

### 6、拦截器

~~~javascript
// 1.添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 2.添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  });


// 3.封装的方法
export function setRequest(config) {

    const instancel = axios.create({
        baseURL: 'http://127.0.0.1:8888/api/private/v1/',
        timeout: 5000
    })

    instancel.interceptors.request.use(config => {
        NProgress.start();
        config.headers.Authorization = sessionStorage.getItem('token')
        return config
    })


    instancel.interceptors.response.use(config => {
        NProgress.done();
        return config
    })

    return instancel
}
~~~

### :star:Vuex

~~~javascript
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(vuex)

// index.js
const store = new Vuex.Store({
 	getters,
	modules:{
		demo1
	}
 },
// getters.js
const getters = {
	userName:state => state.demo1.userName,
    password:state => state.demo1.password
}
// modules/demo1.js
const state = {
    userName:'admin',
    password:123456
}
const getter = {
	getInfo(state,getters)
}
const mutations = {
    Get_Info(state,提交接收的参数)
}
const actions = {
    Get_Info({commit},payload)
}
export.default {
	namespaced:true
	state,
	getters,
	mutations,
	actions
}
...mapMutations("user", ["getInfo"]),
...mapState({
      name: (state) => state.user.name,
}),
~~~