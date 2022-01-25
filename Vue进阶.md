

# Vue进阶

## 1.vue-cli脚手架

### 1.1 什么是vue-cli脚手架?

**CLI**   Command-Line Interface 命令行界面，俗称脚手架

![](D:\系统默认\图片\Saved Pictures\脚手架.jpg)

🎨这里用的是4.x的新版本

> 关于旧版本
>
> Vue CLI 的包名称由 `vue-cli` 改成了 `@vue/cli`。 如果你已经全局安装了旧版本的 `vue-cli` (1.x 或 2.x)，你需要先通过 `npm uninstall vue-cli -g` 或 `yarn global remove vue-cli` 卸载它。
>
> Node 版本要求
>
> Vue CLI 4.x 需要 [Node.js](https://nodejs.org/) v8.9 或更高版本 (推荐 v10 以上)。你可以使用 [n](https://github.com/tj/n)，[nvm](https://github.com/creationix/nvm) 或 [nvm-windows](https://github.com/coreybutler/nvm-windows) 在同一台电脑中管理多个 Node 版本。

### 1.2 vue-cli脚手架的作用

能够快速搭建出vue项目的骨架，能够大大增加你的开发效率，让你减少前端项目环境的配置(类似于后端中的**Maven**)

### 1.3 vue-cli脚手架的安装

想要安装 vue-cli脚手架 ，那我得先介绍一下 **Node.js**和**npm**



## 2.Node.js

### 2.1 什么是Node.js?

**看看官方的描述**

> Node.js是一个Javascript运行环境(runtime environment)，不是一个js文件，实质是对Chrome V8引擎进行了封装。Node.js 是一个让 JavaScript 运行在服务端的开发平台，它让 JavaScript 成为与PHP、Python 等服务端语言平起平坐的脚本语言。
> Node.js提供替代的API，使得V8在非浏览器环境下运行得更好。V8引擎执行Javascript的速度非常快，性能非常好。 
> Node.js是一个基于Chrome JavaScript运行时建立的平台， 用于方便地搭建响应速度快、易于扩展的网络应用

**总结来说**:Node.js就是一个JavaScript的运行环境，能够让JavaScript脱离浏览器独立在服务端运行🐱‍🏍

### 2.2 安装Node.js

🌍官网地址：https://nodejs.org/zh-cn/

![image-20220116124651224](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220116124651224.png)

点进去最新版本,下载安装一直下一步就好啦！

### 2.3 测试Node.js是否安装成功

打开cmd命令行输入 node -v 出现版本号则安装成功!

![](D:\系统默认\图片\Snipaste_2022-01-16_12-51-09.png)







## 3.npm

### 3.1 什么是npm

npm是Node.js内置的工具,可以用来下载与管理如jquery.js这一类的第三方包（类似于linux的rpm）

这里我们使用npm来安装vue-cli脚手架

### 3.2 npm常用命令



- `npm install <xxx> -g`  将包安装到全局环境中
- `npm ls` 列出当前安装的了所有包
- `npm help`  查看npm命令帮助 
- `npm help <命令>`查看某个命令的详情

### 3.3 查看npm全局安装下包的路径

- 使用 `-g` 标志可以执行全局安装

- 通过 `npm config get prefix` 来获取当前设置的全局目录

  

## 4.开始vue-cli脚手架的安装



命令行输入

```bash
npm install -g @vue/cli
```

### 4.1 测试vue-cli是否安装成功

命令行输入

```bash
vue --version
```

![](D:\系统默认\图片\Snipaste_2022-01-16_13-04-30.png)

出现版本信息则安装成功！



## 5.使用vue-cli创建并运行第一个项目



### 5.1 切换安装路径

![](D:\系统默认\图片\Snipaste_2022-01-16_13-10-21.png)



像我这，我要安装到D盘下的WorkSpace\Projects\VsCode\Code路径

### 5.2 创建项目

命令行输入: **vue create 项目名**

例如我这要创建一个叫hello-word的脚手架项目

```bash
vue create hello-world
```

之后会出现这样几个选项

![](D:\系统默认\图片\Snipaste_2022-01-16_13-18-08.png)

如果你只学了vue2就选第一个，学了vue3就选第二个，第二个的模板会多一些东西

**这里我们选第一个**!



### 5.3 安装完成！

安装完成后,目录里面会多出一个文件夹



![](D:\系统默认\图片\Snipaste_2022-01-16_13-26-56.png)

### 5.4 目录结构

我们通过VsCode打开看看

![](D:\系统默认\图片\Snipaste_2022-01-16_13-48-26.png)



这个目录结构非常重要，就像maven一样，我们要把对应的资源放到对应的目录中,以起到规范作用，同时避免不必要的错误发生!

### 5.5 运行项目

创建成功项目后，命令行会变成这样

![](D:\系统默认\图片\Snipaste_2022-01-16_14-07-27.png)

**第一步**：我们cd 进我们想要运行的项目

```bash
cd hello-word
```

第二步:输入 运行命令

```
npm run serve
```

执行完后会出现两个地址

![](D:\系统默认\图片\Snipaste_2022-01-16_14-13-27.png)

随便一个复制进浏览器就可以访问啦！（❗有的会是8080端口,但不用担心,npm很智能,会自动分配没有被占用的端口,因为我这里的8080端口被占用了）

**访问结果**

<img src="C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220116141716512.png" alt="image-20220116141716512" style="zoom: 50%;" />

**结束运行**：在命令行里面 ctrl+c 然后再Y





## 6.注册组件

### 6.1 什么是组件?

组件是可复用的 [Vue](https://so.csdn.net/so/search?q=Vue&spm=1001.2101.3001.7020) 实例, 把一些公共的模块抽取出来，然后写成单独的的工具组件或者页面，在需要的页面中就直接引入即可那么我们可以将其抽出为一个组件进行复用。例如 页面头部、侧边、内容区，尾部，上传图片，等多个页面要用到一样的就可以做成组件，大大提高了代码的复用率

![](D:\系统默认\图片\Snipaste_2022-01-16_14-54-23.png)

一个vue组件通常由三部分构成:

**html部分**:在template标签中可以定义html代码 （❗标签里必须有一个div作为大盒子）

**js部分**：vue代码部分，包括data，created，methods，computed，watch等实例属性

**css部分**:定义css样式

​	👀**Vue组件模板**

```javascript
<template>
    <div>
    
  </div>
</template>
<script>
export default {
  data() {
   return {

   }

  },

  created(){

  },

  computed:{

  },

  methods:{

  },

}

</script>

<style lang="css" scoped>

</style>
```



### 6.2 全局注册组件	

*全局注册后，该组件在任何地方都可以使用*

以我要在App.vue中使用Header.vue组件为例

**第一步**: 在**main.js**中导入并注册组件

<img src="D:\系统默认\图片\Snipaste_2022-01-16_15-07-49.png" style="zoom: 67%;" />

**第二步**:使用	

![](D:\系统默认\图片\Snipaste_2022-01-16_15-09-05.png)

在其他组件的**template**中以标签的形式使用即可！

### 6.3 本地注册组件

*在组件的内部去注册另外一个组件，只有在该组件内才有效*

![](D:\系统默认\图片\Snipaste_2022-01-16_15-27-36.png)





## 7.组件之间的参数传递

### 父传子

通过子组件的props部分，来指明可以接收的参数，父组件通过在标签中写明参数的键值对来传递参数

![image-20220116154448711](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220116154448711.png)

### 子传父

![image-20220116160220657](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220116160220657.png)





## 8.Axios

### 8.1 什么是Axios？

> [Axios](https://so.csdn.net/so/search?q=Axios&spm=1001.2101.3001.7020) 是一个开源的可以用在浏览器端和 NodeJS 的异步通信框架，她的主要作用就是实现 A JAX 异步通信，其功能特点如下：
> 拦截请求和响应
> 转换请求数据和响应数据取消请求
> 自动转换 JSON 数据
> 客户端支持防御 XSRF （跨站请求伪造）

🔻诚然,jquery的ajax也很好用,但是由于vue的盛行，我们不可能为了用ajax去单独引入一个jquery库，所以axios这样的轻量级异步通信框架就诞生了

### 8.2 安装Axios

🌍官网地址:http://www.axios-js.com/

使用 npm:

```
 npm install axios
```

使用 cdn:

```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

如果想全局引用cdn需要将其放在index.html中

🎂**在main.js中引用**

```javascript
import axios from 'axios'
Vue.prototype.$axios = axios
```

### 8.3 使用Axios发送Get请求

✨Axios发送请求的方式有几种,这里只提供一种，想要了解可以去🌍官网http://www.axios-js.com/

#### Get请求和Post请求

```javascript
this.$axios({
   //这里的get修改为post则为post请求
 method: 'get',
    //需要请求的url
 url: 'http://localhost:8087/vue',   //此时会将baseURL与该url进行拼接成最终请求的url
    //携带参数,后端可以request.getParameter接收,也可以以形参的形式接收
 params:{
  page:1,
  count:2,
  type:'video'
 }
//这里的response是后台回调的值
}).then(response=>{
//回调函数
alert(response.data)

})

```

### 8.4 跨域问题

🎨**什么是跨域**？

> 跨域，指的是浏览器不能执行其他网站的脚本。它是由浏览器的同源策略造成的，是浏览器施加的安全限制。
>
> 同源:**域名，协议，端口 都相同
>
> 跨域:**域名，协议，端口**中一项或多项不同
>
> http://www.4399.com/index.html 请求 http://www.4399.com/login.html 非跨域
>
> http://www.4399.com/index.html 请求 http://www.7k7k.com/login.html 跨域 **主域名**不同 
>
> http://abc.4399.com/index.html 请求 http://defg.4399.com/login.html 跨域 **子域名**不同
>
> http://www.4399.com:8080/index.html 请求 http://www.4399.com:8081/login.html 跨域 **端口**不同
>
> http://www.4399.com/index.html  请求 https://www.4399.com/login.html   跨域 协议不同
>
> ❗请注意：localhost和127.0.0.1端口虽然都指向本机，但也属于跨域。
>
> 浏览器执行javascript脚本时，会检查这个脚本属于哪个页面，如果不是同源页面，就不会被执行。

#### 解决跨域问题

##### **springmvc**:

在springmvc配置文件中加入

```xml
<!-- 接口跨域配置 -->
<mvc:cors>
    <mvc:mapping path="/**"
                 allowed-origins="*"
                 allowed-methods="POST, GET, OPTIONS, DELETE, PUT"
                 allowed-headers="Content-Type, Access-Control-Allow-Headers, Authorization, X-Requested-With"
                 allow-credentials="true" />
</mvc:cors>
```

**springboot:**

在配置类中

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
@Configuration
public class CorsConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("*")
                .allowedMethods("GET", "HEAD", "POST", "PUT", "DELETE", "OPTIONS")
                .allowCredentials(true)
                .maxAge(3600)
                .allowedHeaders("*");

    }
}
```





## 9.vue-router路由

### 9.1 什么是路由？

> vue-router是Vue.js官方的路由插件，它和vue深度集成,以用于设定访问路径，以往的页面都是通过**<a></a>**标签来进页面跳转的
>
> 由于vue中各个页面都是以组件的形式进行拼接，所以无法用传统的方式进行页面跳转，从而vue官方引入的vue-router来解决这个问题
>
> 🌍官网地址:https://router.vuejs.org/zh/

### 9.2 安装vue-router路由

npm:

```bash
npm install vue-router
```

cdn:

<script src="https://cdn.bootcdn.net/ajax/libs/vue-router/3.5.3/vue-router.common.js"></script>

### 9.3 使用路由跳转页面

**第一步**:在src下创建一个静态路由表 **routes.js**

```javascript
// 1 导入组件
import Context from './components/Context.vue'
import Header from './components/Header.vue'
//2 引入路由模块,这里以数组的形式,用逗号分割
export const routes=[{
    path: '/toHeader', //所需要路由的路径,通过这个路径可以访问到Header组件
    component: Header //添加被该路径访问的组件
},{
    path: '/toContext', 
    component: Context 
}
]
```

**第二步**:在main.js中配置

```javascript
//3 引入路由模块,这相当于引入vue-router这个插件
import VueRouter from 'vue-router'
//4 让vue能够使用 VueRouter
Vue.use(VueRouter)
//5 引入第一步配置的routes.js静态路由表
import {routes} from './routes'
//6 创建一个VueRouter模块实例
 const router = new VueRouter({
  routes:routes
});
//7 将routes放入vue对象中
new Vue({
  router,//只需这里加上就好了！
  render: h => h(App), 

}).$mount('#app')
```

**使用**:

**1**.**使用html标签进行页面跳转**：在其他组件里，通过`<router-link to="路由表里配置的路径"></router-link>` 即可进行页面跳转,类似于html中的a标签

通过 `<router-view></router-view>` 标签来显示跳转后的组件

**2**.**js进行页面跳转:**在js方法中直接进行页面跳转 `this.$router.push('/toLoginSuccess');`,在需要显示的位置使用`<router-view></router-view>`

场景：登录成功后需要跳转页面

### 9.4 路由中的参数传递

##### **第一种**: 通过动态路由传递

我们经常需要把某种模式匹配到的所有路由，全都映射到同个组件。例如，我们有一个 `User` 组件，对于所有 ID 各不相同的用户，都要使用这个组件来渲染。那么，我们可以在 `vue-router` 的路由路径中使用“动态路径参数”(dynamic segment) 来达到这个效果：

```js
const User = {
  template: '<div>User</div>'
}

const router = new VueRouter({
  routes: [
    // 动态路径参数 以冒号开头
    { path: '/user/:id', component: User }
  ]
})
```

现在呢，像 `/user/123` 和 `/user/456` 都将映射到相同的路由。

一个“路径参数”使用冒号 `:` 标记。当匹配到一个路由时，参数值会被设置到 `this.$route.params`，可以在每个组件内使用。于是，我们可以更新 `User` 的模板，输出当前用户的 ID：

```js
const User = {
  template: '<div>User {{ $route.params.id }}</div>'
}
```

##### **第二种**: 通过params进行参数传递

1. 在路由组件中设置name属性

![image-20220124222737274](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220124222737274.png)'

2.router-link中绑定to

![image-20220124222922034](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220124222922034.png)

也可以在js代码中

```js
this.$router.push({ name:'name' ,params:{id:1,username:张三}});
```

3 参数获取

![image-20220124223040156](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220124223040156.png)



##### **第三种**: query进行参数传递

路由组件

![image-20220124223911803](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220124223911803.png)

1.router-link中绑定to

![image-20220124224403880](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220124224403880.png)

也可以在js代码中

```js
this.$router.push({ path:'/toLogin' ,query:{id:1,username:张三}});
```

2.参数获取

![image-20220124224845096](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220124224845096.png)



#### params与query的区别

> params与query的区别相当于请求中post和get的区别
>
> params的参数不会在url中显示
>
> query的参数会在url中显示

### 9.5 嵌套路由

 在已经进行路由跳转的页面原有的基础上还能够再进行路由

```text
/user/foo/profile                     /user/foo/posts
+------------------+                  +-----------------+
| User             |                  | User            |
| +--------------+ |                  | +-------------+ |
| | Profile      | |  +------------>  | | Posts       | |
| |              | |                  | |             | |
| +--------------+ |                  | +-------------+ |
+------------------+                  +-----------------+
```

```js
const router = new VueRouter({
  routes: [
    {
      path: '/user/:id',
      component: User,
      children: [
        {
          // 当 /user/:id/profile 匹配成功，
          // UserProfile 会被渲染在 User 的 <router-view> 中
          path: 'profile',
          component: UserProfile
        },
        {
          // 当 /user/:id/posts 匹配成功
          // UserPosts 会被渲染在 User 的 <router-view> 中
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})
```

### 9.6 路由重定向

在vue中重定向指：通过不同路径访问同一组件

**重定向的配置**

```js
const router = new VueRouter({
  routes: [{path:'/toindex',component:index},
           //配置index组件的重定向,这里的redirect与被配置组件的path一致
    { path: '/toindex2', redirect: '/toindex' }
  ]
})
```

重定向的目标也可以是一个命名name的路由：

```js
const router = new VueRouter({
  routes: [{path:'/toindex',name:'index',component:index},
    { path: '/toindex2', redirect: { name: 'index' }}
  ]
})
```

## 10.Element-ui

**第一步**：安装

```
npm i element-ui -S
```

**第二步**：**在main.js**中引入

```js
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

Vue.use(ElementUI);
```





















