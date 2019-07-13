---
title: Vue.js快速入门
date: 2018-07-10 21:33:58
tags:
---

# Vue.js快速入门

## 第一章 Vue.js概述

### 1.1 单页应用的出现

随着移动电话的普及和微信的流行,很多的Wap(H5)应用也随之出现了.使用传统的Webpack技术开发的网页,在手机端的表现往往特别差.

* 传统技术的特点是:
  * 点击某个链接/按钮,或者提交表单后,Webpack页面整体刷新,每次整体刷新都要导致浏览器重新加载对应的内容,特别卡顿.
  * js/css的请求往往很多,过百是很长见的事情.每次打开页面会发送上百次请求,会使网页的打开速度很慢.

这时**单页应用(Single Page App, SPA)**就体现出他的优势

* 页面上局部刷新的,响应速度快,不需要每次加载所有的JS/CSS.
* 前后端分离,前端(手机端)不受(服务器端的)开发语言的限制.

越来越多的App采用SPA的架构.如果你的项目要用在H5上,那么一定要使用单页应用框架,如Angular,React,Vue.js都是很好的框架.

### 1.2 单页应用框架对比

* Angular: 老牌框架.源于google.难学,难用.文档垃圾.不推荐使用.

* React: twitter推出的开源框架.比angular简单些.但最大的弱点:html代码居然要写在js文件中.无法调试.大家不习惯把前后端代码写在一起的风格.所有使用过传统web框架的人(java,rails,php)都觉得奇怪.最大的优点:react native.可以把js代码转换成native app(安卓,ios).(效果会打折扣,也不会100%能转化).能力有限.

* Vue.js: 最大的优点:好学,好用.

  >用到vue的项目:滴滴,饿了吗,阿里的weex,GitLab,大疆,Facebook,新浪微博等等.



## 第二章 基本知识

### 2.1 如何阅读官方文档

我们在查看Vue.js官方文档的时候,会发现他跟我们真正的项目代码完全不一样.原因是在于我们在实际的项目中使用了vue-loader,他可以非常好的帮我们自动加载所有的内容,按照webpack + vue的约定.

### 2.2 webpack

webpack是一种工具,可以把各种js/css/html代码最后打包编译到一起.

Vue.js已经集成了这个工具,我们在使用vue-cli的时候,就会根据命令生成webpack所要求的文件结构,然后在打包的时候(npm run build),vuejs的代码就会被webpack打包成正常的html代码和文件目录.本书中所讲的知识,都是"基于webpack的vue.js"

### 2.3 安装

安装:略

试运行:1,创建一个基于webpack模板的新项目:

>````js
>$ vue init webpack my-project
>````

注意:我们使用vue都是在**webpack**的大前提下使用的.

2,安装依赖:

> ````js
> $ cd my-project
> $ npm install
> ````

3,在本地,以默认的端口来运行:

> ````js
> $ npm run dev
> ````

### 2.4 Webpack下的Vue.js项目文件结构

全局的文件结构如下:

1. **build/**                        //编译用到的各种打包脚本.不可或缺,不要随意修改

   * build.js     			//打包使用,不要修改	
   * check-versions.js             //检查npm版本,不要修改
   * dev-client.js                      //是开发时使用的服务器脚本,不要修改
   * dev-server.js                     //是开发时使用的服务器脚本,不要修改
   * utils.js                                //不要修改,做一些css/sass等文件的生成
   * vue-loader.conf.js              //**非常重要的配置文件,不要修改**,内容是用来辅助加载Vue.js用到的css source map等内容的.
   * webpack.base.conf.js        //基本的配置文件,不要修改
   * webpack.dev.conf.js           //基本的配置文件,不要修改
   * webpack.prod.conf.js         //基本的配置文件,不要修改

2. **config/ **                       //跟部署和配置相关

   * dev.env.js                  //开发模式下的配置文件,一般不用修改
   * prod.env.js                //生产模式下的配置文件,一般不用修改
   * index.js                     //很重要的文件,定义了开发时的端口(默认是8080),定义了图片文件夹(默认static),定义了开发模式下的代理服务器.**我们修改的还是比较多的**

3. **dist/**                            //打包后的文件夹

   * static/

     * css/
       * app.xxxxx.css
       * app.xxxxx.css.map
     * js/
       * app.xxxxx.js
       * app.xxxxx.js.map
     * index.html

     <table><tr><td bgcolor=yellow><font color=red>可以看到,对应的css,js,map文件都在这里.这个文件不要放在git中</font></td></tr></table>

4. **node_modules/**          //node第三方包,特别多,特别大.**$ npm install**所产生,这个文件夹不要放在git中.

5. **src/ **                            //源代码

   <table><tr><td bgcolor=yellow><font color=red>最最核心的源代码所在的目录</font></td></tr></table>

   * src/
     * assets/
       * logo.png
     * components/
       * Book.vue
       * BookLIst.vue
       * Hello.vue
     * router/
       * index.js
     * App.vue
     * main.js

   >assets:用到的图片
   >
   >components:用到的"视图"和"组件"所在的文件夹
   >
   >router/index.js路由文件.定义了各个页面对应的url
   >
   >App.vue 如果index.html是一级页面模板的话,这个App.vue就是二级页面模板.所有的其他vue.js页面,都作为该模板的一部分被渲染出来
   >
   >main.js 废代码.没有实际意义,但是为了支撑整个vue.js框架,存在很必要.

6. **static/ **                        //静态文件,暂时无用

7. **index.html **                //最外层文件

8. **package.json**            //node项目配置文件

### 2.5 创建一个页面

创建页面需要两步:

1. 新建路由
2. 新建vue页面

#### 2.5.1 新建一个路由

路由文件是src/router/index.js,打开之后,我们增加两行:

> ````js
> import Vue from 'vue'
> import Router from 'vue-router'
> import HelloWorld from '@/components/HelloWorld'
> //增加这一行,作用是引入SayHi这个component
> import SayHi from '@/components/SayHi'
> 
> Vue.use(Router)
> 
> export default new Router({
>   routes: [
>       
>       //增加下面几行,表示定义了 /#/say_hi 这个url
>     {
>         path: '/say_hi',
>         name: 'SayHi',
>         component: SayHi
>           
>      },
>     {
>       path: '/',
>       name: 'HelloWorld',
>       component: HelloWorld
>     }
>   ]
> })
> 
> 
> ````

#### 2.5.2 创建一个新的component

我们要创建src/components/SayHi.vue,这个文件

如下:

> ````js
> <template>
>     <div>
>     	Hi Vue!
>     </div>
> </template>
> 
> <script>
>     export default {
> data () {
>     return { }
> }
>     }
> </script>
> 
> <style scoped>
> 
> </style>
> 
> ````

现在,我们可以直接访问http://localhost:8080/#/[say_hi](http://localhost:8080/#/say_hi) 这个链接了

* <template></template>代码段中,表示的是HTML模板.

* <script> </script>表示的是js代码,所有的js代码都写在这里 .

* <style></style>表示所有的CSS/SCSS/SASS文件都可以写在这里.

#### 2.5.3 为页面增加一些样式

例如,我们可以在页面加一些样式

> ````js
> <template>
>   <div class="hi">
>     Say Hi!
>   </div>
> </template>
> 
> <script>
>   export default {
>     name: "SayHi"
>   }
> </script>
> 
> <style scoped>
>   .hi {
>     color: red;
>     font-size: 20px;
>   }
> </style>
> ````

#### 2.5.4 在页面中定义并显示变量

如果要在vue页面中定义一个变量,并把它显示出来,就需要事先在data中定义:

> ````js
> <template>
>   <div class="hi">
>     Say Hi!
> <!--    步骤2: 在这里显示 message-->
>     {{message}}
>   </div>
> </template>
> 
> <script>
>   export default {
>     name: "SayHi",
>     data () {
>       return {
>         //步骤1: 这里定义了变量 message 的初始值
>         message: '你好Vue! 本消息来自于变量'
>       }
>     }
>   }
> </script>
> 
> <style scoped>
>   .hi {
>     color: red;
>     font-size: 20px;
>   }
> </style>
> ````

### 2.6 语法简写说明

#### 2.6.1 import

import用来引入 第三方程序

> ```` js
> import Vue from 'vue'
> import Router from 'vue-router'
> ````

上面两个是引入package.json中的第三方包,所以可以直接import ... from <包名>

> ````js
> import SayHi from '@/components/SayHi'
> ````

上面这个,在from后面,有@符号,表示是在本地文件系统中,引入文件.@代表源代码的目录,一般是src.在@出现之前,我们在编码的时候也会这样写:

> ````js
> import Swiper from '../components/swiper'
> import SwiperItem from '../conponents/swiper-item'
> import XHeader from '../connponents/header/x-header'
> import store from '../vuex/store'
> ````

这种方式大量使用了../..这样的代码,会引起代码的混乱.**所以推荐使用@方法**

#### 2.6.2 export default {...}

我们会看到,在每个vue文件中的<script>代码端中,都会存在这个代码.<font color="yellow">它的作用是方便其他代码对这个代码的引用.</font>

对于vue程序员来说,我们就记住这个写法就行.没他不行,有他意义也不大.

在ES6之前的js没有一个统一的模块定义方式,流行的定义方式有AMD,CommonJS等,而**ES6从语言层面对定义模块的方式进行了统一**.

假设有:lib/math.js 文件内容如下:

>````js
>export function sum(x,y) {
>    return x + y
>}
>export var pi = 3.1415926
>````

app.js文件内容如下:

> ````js
> import * as math from "lib/math"
> alert("2π = " + math.sum(math.pi,math.pi))
> ````

other_app.js文件内容如下:

> ````js
> import {sum,pi} from "lib/math"
> alert("2π = " + math.sum(pi,pi))
> ````

#### 2.6.3 一些简写 

我们会发现下面的代码:

````js
<script>
export default {
   data () {
     return { }
   }		
}   
</script>
````

实际上,上面的代码是一种简写的形式,他等同于下面的代码:

````js
<script>
export default {
   data: function() {
     return { }
   }		
}   
</script>
````

#### 2.6.4let,var,常量与全局变量

声明本地变量,使用let或者var.两者的区别是:

* var:有可能引起变量提升,或者 块级作用域的问题
* let:就是为了解决这两个问题的存在

最佳实践:多用let,少用var.遇到诡异变量问题的时候,就查查是不是var的问题.

<font color ="yellow">记得,在webpack中,使用任何变量都要使用var或者let来声明,常量使用const.</font>

对于全局变量,直接在index.html中声明即可

> ```
> window.title = '我的博客列表'
> ```

### 2.7 Vue.js渲染页面的过程和原理

#### 2.7.1 渲染过程

1,最初的最初,我们要知道./build/webpack.base.conf.js这个文件,是webpack打包的主要配置文件

其中:

> ````js
> module.exports = {
>     entry : {
>         app: './src/main.js' //这里就定义了vue的 入口文件
>     }
> }
> ````

2,找到index.html,可以看到内容如下:

> ````js
> <body>
>     <div id="app"></div>
> </body>
> ````

<font color="yellow">这里的id='app',就是将来会动态变化的内容.特别类似于rails的layout.只不过这个layout是第一层layout(最大的layout)</font>

3,回到src/main.js

> ````js
> import Vue from 'vue'
> import App from './App'
> import router from './router'
> 
> new Vue({
>     el: '#app', //这里,#app对应的就是<div id="app"></div>
>     router,
>     template: '<App/>'
>     components: { App }  //这里,App就是./src/App.vue
> })
> ````

<font color="#782">熟悉jquery,css选择器的同学可以看到,el:"#app"就是index.html中的<div id= app></font>

4,注意上面的App.vue,他会被main.js加载,App.vue的内容如下:

> ````js
> <template>
>   <div id="app">
>         <router-view class="view"></router-view>
>   </div>
> </template>
> <script>
> 
> </script>
> <style>
> </style>
> ````

注意上面的template,这就是第二层的layout,可以看到,里面还有一个div id = 'app',这个元素跟index.html中的是同一个元素(暂且这么理解)

所有的<router-view>中的内容,都会被自动替换

<script>中的代码则是脚本代码.至此整个过程结束了

#### 2,7.2 原理

Vue.js就是典型的Ajax工作方式:只渲染部分页面.

页面从来不会刷新.所有页面的变化,都限定在index.html中的下列代码中:

> ````js
> <div id = "app"></div>
> ````

所有的动作可以靠url来触发,例如:

>* /#/books_list 对应某个列表详情页
>* /#/books/3 对应的某个详情页

### 2.8 视图中的渲染

#### 2.8.1 渲染某个变量

假定我们定义了一个变量:

>````js
><script>
>export default {
>	data () {
>        return {
>             my_value: '默认值',
>        }
>	}
>}
></script>
>````

我们就可以这样显示它:

```` js
<div> {{  my_value }} </div>
````

#### 2.8.2 方法的声明和调用

声明一个方法:  show_my_value

> ````js
> <script>
> export default {
>   data () {
>     return {
>       my_value: '默认值',
>     }
>   },
>   methods: {
>     show_my_value: function(){
>       // 注意下面的　this.my_value, 要用到this这个关键字．
>       alert('my_value: ' + this.my_value);
>     },
>   }
> }
> </script>
> ````

调用该方法:

> ````js
> <template>
>   <div>
>     <input type='button' @click="show_my_value()" value='...'/>
>   </div>
> </template>
> ````

对于有参数的方法,直接传递参数就好了.

> ````js
> <template>
>   <div>
>     <input type='button' @click="say_hi('Jim')" value='...'/>
>   </div>
> </template>
> <script>
> export default {
>   data () {
>     return {
>       my_value: '默认值',
>     }
>   },
>   methods: {
>     say_hi: function(name){
>       alert('hi, ' + name)
>     },
>   }
> }
> </script>
> ````

#### 2.7.3 事件处理 v-on

我们看到,很多时候,@click等同于 v-on:click,下面两个是一样的:

> ````js
> <input type="button" @click="sayHi('zhangsan')>
> <input type="button" v-on:click = "sayHi('zhangsan)">
> ````

以上就是我们实际当中最常见的用法.