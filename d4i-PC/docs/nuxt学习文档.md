> ### 为什么选择nuxt.js

  现在我们的项目大多数都是spa（单页面应用），感觉单页面应用比之前的模板渲染要好很多，首先单页面应用是前后端分离，架构清晰，前端负责交互逻辑，后端负责数据，前后端单独开发，独立测试。
  
  但是，SPA不利于SEO（搜索引擎优化）。
  
  那么为什么要做SEO？做SEO有什么好处？简单来说SEO是一种利用技术手段提升网站在搜索引擎之中的排名的方式，让搜索引擎更为信任网站，通过提升排名获得更多网站流量。
  
  在我们开发的过程中，我们有 SEO 的需求，我们需要搜索引擎更多地抓取到我们的项目内容，此时我们需要SSR。SSR保证用户尽快看到基本的内容，也使得用户体验性更好。
  
  SSR： 服务端渲染（Server Side Render），即：网页是通过服务端渲染生成后输出给客户端。比如JSP、PHP、JavaWeb等都是SSR架构，也就是服务端取出数据和模板组合生成 html 输出给前端，前端发生请求时，重新向服务端请求 html 资源，路由也由服务端来控制。
  
  ==Nuxt.js是使用 Webpack 和 Node.js 进行封装的基于Vue的SSR框架，不需要自己搭建一套 SSR 程序，而是通过其约定好的文件结构和API就可以实现一个首屏渲染的 Web 应用。==
 
> ### 创建nuxt项目模板

1. 创建nuxt基础模板

>  vue init nuxt-community/starter-template <project-name>

2. 创建nuxt+express模板

> vue init nuxt/express <project-name>

3. 更多的模板

![image.png](http://note.youdao.com/yws/res/496/WEBRESOURCE2ef44ee00b8caba2d5a6f20489b18ba7)

> ### 目录结构
- ==assets== 需要编译的资源文件，如 JavaScript、SASS、LESS 等。
- ==static== 不需要编译的静态资源文件，如图片资源。
- ==components== 顾名思义，存放 *.vue 组件的地方。一般用来存放非页面级别的组件，如 header、footer 等公共组件，该目录下的组件具有常规 vue 组件的方法和特性，不会被 nuxt.js 扩展特性
- ==layouts== 布局目录，设置布局的地方，其中 <nuxt/>     标签是我们写的页面内容。可用作添加导航栏、底部栏等截面。
- ==middleware== 中间件目录，所谓中间件，就是在页面与页面跳转中执行的函数方法。如页面跳转时验证用户信息操作。
- ==pages== 用于存放页面级别的组件。该目录下的文件会转换成相应的路由路径供浏览器访问。另外呢，该目录下的 *.vue 页面文件中Nuxt.js提供了一些特殊的方法用于处理服务器渲染中的事件。
- ==plugins== 插件目录，像 iview 这种第三方插件就放在这里。
-== store== vuex 状态管理器目录，如果该目录是空的，Nuxt.js将不启用vuex。当我们在该文件夹下创建 index.js 文件后即可使用 vuex 状态管理器
-== nuxt.config.js== 该文件是 Nuxt.js 的唯一配置项，之前提过 Nuxt.js 将 Webpack 等一众配置都封装好了，所以如果需要特殊配置，只需要修改该文件来覆盖默认配置即可


> ### nuxt 生命周期

众所周知，Vue的生命周期全都跑在客户端(浏览器)，而Nuxt的生命周期有些在服务端(Node)，客户端，甚至两边都在:

![image.png](http://note.youdao.com/yws/res/891/WEBRESOURCEe2bb63f8a6a293a5ceb86142f9034264)

==红框内的是Nuxt的生命周期(运行在服务端)，黄框内同时运行在服务端&&客户端上，绿框内则运行在客户端==

==红框、黄框内的周期都不存在Window对象==

```js
export default {
  asyncData() {
    console.log(window) // 服务端报错
  },
  fetch() {
    console.log(window) // 服务端报错
  },
  created () {
    console.log(window) // undefined
  },
  mounted () {
    console.log(window) // Window {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, frames: Window, …}
  }
}
```

> ### nuxt.config.js 介绍

1.全局css的使用

```js
 css: ["~/assets/css/main.scss"]
```

2.页面的loading效果

```js
loading: false // 禁用

loading: { color: '#3B8070' }//颜色条

loading: '~components/loading.vue'//使用组件
```

3. 如何添加自己封装的插件

~plugins/main.js 文件：
```js
import Vue from "vue";
import "reset.css";
import index from "../assets/js/index.js";
import utility from "../assets/js/utility/index.js";
import { EventBus } from "@/assets/js/event-bus.js";
import VueCookies from "vue-cookies";

Vue.prototype.$VueCookies = VueCookies;
require("es6-promise").polyfill();
Vue.use(index);//封装的组件
Vue.prototype.$util = utility; //全局方法
Vue.prototype.$eventBus = EventBus;
```
~plugins/message.js文件（只在客户端使用）：
```js
import Vue from "vue";
import message from "../components/message/index.js";
Vue.use(message);
import VueQr from "vue-qr";
Vue.use(VueQr);
```

```js
plugins: [
    { src: "~plugins/main", ssr: true },//true 代表客户端 服务端都能使用
    //message在组件封装时使用了window对象，ssr只能为false
    { src: "~plugins/message", ssr: false },//false 代表只在客户端使用
    
    { src: "~plugins/axios", ssr: true },
    { src: "~plugins/router", ssr: false }
    
 ],
 ```
==ps:新建项目生成的~plugins/axios.js文件做全局拦截器：==
```js
export default function ({$axios, redirect, req, store, route, app}) {
     $axios.onRequest(config =>{
         
     })
      $axios.onError(error =>{
       const code = parseInt(error.response && error.response.status);
        if (code === 400) {
           redirect("/"); //服务端报错重定向到首页
         }
     })
}

参考：
export default function (app) {
  let axios = app.$axios; 
 // 基本配置
  axios.defaults.timeout = 10000
  axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded'

  // 请求回调
  axios.onRequest(config => {})

  // 返回回调
  axios.onResponse(res => {})

  // 错误回调
  axios.onError(error => {})
}
 ```
4. 如何拓展 webpack 配置

```js
  build: {
    vendor: ["@babel/polyfill", "event-source-polyfill", "axios"],/*多个地方引用，防止多次打包*/
    //扩展webpack配置
    extend(config, { isClient }) {
      console.log({ isClient });
      // 为 客户端打包 进行扩展配置
      if (isClient) {
        config.devtool = "eval-source-map";
      }
    }
  },
```
> ### 中间件的使用做路由保护

~middleware/auth.js文件：

```js
export default async function({ $axios, redirect, req, store, route, app }) {
  if (process.client) {
    if (!store.state.userInfo.id) {
      return redirect("/");
    }
  }

  if (process.server) {
    let token = getCookie("token", req).replace(/%20/, "");
    if (getCookie("token", req)) {
      const res = await getUserInfo($axios, token);
      if (!res) {
        return redirect("/");
      }
    } else {
      return redirect("/");
    }
  }
}
```
在组件中使用

```js
export default {
  middleware: "auth",  // 路由保护
  
}
```
> ### asyncData

1.一个请求

```js
    asyncData({$axios}) {
      return HOME.GET_MATRIX($axios).then(res => {
        if (res.status == STATUS_CODE.SUCCESS) {
            
         });
     });
    return {data: dataSource, column: dataColumn}
        }
      });
    },

```

2.多个并发请求

```js
async asyncData({ query, $axios }) {

 let [res01, res02, res03] = await Promise.all([
      DATASET_LIST.GET_DATASET_SUMMARY(queryData, $axios),
      DATASET_LIST.GET_DATASET_LIST({ sort: "UPDATEAT", ...queryData }, $axios),
      DATASET_LIST.GET_CATEGORY_LIST(data, $axios)
    ]);
    
    //对response操作
    
     return {datasetSummary: res01.data,};
    }
 
```
==asyncData接收的常见的几个参数：==
```js
   asyncData({app, isDev, route, store,env, params, query,req, res,redirect,error }) {
   
    }
  },
```

> ### Meta标签

nuxt.config.js文件默认Meta标签：
```js
module.exports = {
 head: {
    // title: pkg.name,
    title: "数工场_持续汇集可靠而安全的工业开放数据。",
    meta: [
      { charset: "utf-8" },
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        hid: "description",
        name: "description",
        content:
          "数工场是中云数据结合自身在工业大数据领域的深厚积累，基于工业机理构建的工业知识图谱，打造的实现工业开放数据集有效聚合的数据共享平台，致力于企业内部数据融合、工业开放数据聚合及产业链数据共享，助力智能制造。"
      },
      {
        hid: "keywords",
        name: "keywords",
        content: "数工场,中云数据,工业数据集,工业开放数据,数据集市,工业数据报告"
      }
    ],
    link: [{ rel: "icon", type: "image/x-icon", href: "/favicon.ico" }],
    script: [
      {
        src: "/browser-update.js",
        type: "text/javascript",
        charset: "utf-8"
      }
    ],   //全局引入的script标签  做低版本浏览器提示
    __dangerouslyDisableSanitizers: ["script"]
  },
}
```
页面组件特有的Meta标签:

```js
export default {
    head() {
      return {
        title: this.industryName+" - "+this.getCategoryName+" - 数工场_持续汇集可靠而安全的工业开放数据。",
        meta: [
          {hid: 'description', name: 'description', content: `${this.datasetSummary.description}`},
        ]
      }
    },
}
```

> ### 使用Vuex

nuxt自己集成了vuex，所以不需要安装，在/store目录下新建index.js即可使用

```js
import Vuex from 'vuex'

let store = () => new Vuex.Store({
  state: {
    token: ''
  },
  mutations: {
    setToken (state, token) {
       state.token = token
    }
  }
})

export default store

```





> ### 常见问题总结：

1.Window 或 Document 对象未定义？

在引入第三方插件，或者直接在代码中写 window 时，控制台会给出警告，window 未定义。
发生在这个问题的原因时，node服务端并没有window 或 document 对象。解决方法，通过 process.browser 来区分环境。

```js
if (process.browser) {
 // 引入第三方插件
 require('***')
 // 或者修改window对象下某一属性
 window.mbk = {}
}
```






> ### 推荐文章：

1. [nuxt知识图谱](https://blog.csdn.net/komojay/article/details/79545297)
2. [高仿掘金demo](https://github.com/xuqiang521/nuxt-ssr-demo)
3. [nuxt.js配置BASE_URL（基本域名）和NODE_ENV（环境变量）](https://blog.csdn.net/qq_21363577/article/details/87899591)