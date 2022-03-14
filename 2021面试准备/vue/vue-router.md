# hash模式

- 定义：`hash` 模式是一种把前端路由的路径用井号 `#` 拼接在真实 `url` 后面的模式。当井号 `#` 后面的路径发生变化时，浏览器并不会重新发起请求，而是会触发 `onhashchange` 事件。

- 特点：hash变化会触发网页跳转，即浏览器的前进和后退。

  `hash` 可以改变 `url` ，但是不会触发页面重新加载（hash的改变是记录在 `window.history` 中），即不会刷新页面。也就是说，所有页面的跳转都是在客户端进行操作。因此，这并不算是一次 `http` 请求，所以这种模式不利于 `SEO` 优化。`hash` 只能修改 `#` 后面的部分，所以只能跳转到与当前 `url` 同文档的 `url` 。

  `hash` 通过 `window.onhashchange` 的方式，来监听 `hash` 的改变，借此实现无刷新跳转的功能。

  `hash` 永远不会提交到 `server` 端（可以理解为只在前端自生自灭）。

  

  

# history模式

### api

| API                                       | 定义                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| history.pushState(data, title [, url])    | pushState主要用于**往历史记录堆栈顶部添加一条记录**。各参数解析如下：**①data**会在onpopstate事件触发时作为参数传递过去；**②title**为页面标题，当前所有浏览器都会忽略此参数；③**url**为页面地址，可选，缺少时表示为当前页地址 |
| history.replaceState(data, title [, url]) | 更改当前的历史记录，参数同上； 上面的pushState是添加，这个更改 |
| history.state                             | 用于存储以上方法的data数据，不同浏览器的读写权限不一样       |
| window.onpopstate                         | 响应pushState或者replaceState的调用                          |

### 特点

对于 `history` 来说，主要有以下特点：

- 新的 `url` 可以是与当前 `url` 同源的任意 `url` ，也可以是与当前 `url` 一样的地址，但是这样会导致的一个问题是，会把**重复的这一次操作**记录到栈当中。
- 通过 `history.state` ，添加任意类型的数据到记录中。
- 可以额外设置 `title` 属性，以便后续使用。
- 通过 `pushState` 、 `replaceState` 来实现无刷新跳转的功能。

### 解决刷新404 的问题例如nginx

设置

```nginx
try_files $uri /index.html;

```



# 路由传参

## params

- params传值要传**name**使用**path**会undefined **this.$router.push({name:'re',params:{id:10}})**
- 在route中配不配置/:id/:name等参数会导致其参数**在不在地址栏中显示**
- 在route中配不配置/:id/:name等参数会导致其参数**刷新页面参数会不会消失**
- 取值：**this.$route.params**

## query

- query传值用name或者path都可以
- query不用特殊配置路由
- 刷新页面传参不会消失
- 在url上参数是？key=value&key=value#

# router和route

## router 整个路由实例，可以操控整个路由

```js
this.$router.push
this.$router.go
this.$router.replace
```



## route 是当前路由实例跳转到的对象

```js
this.$route.params
this.$route.path
```

# Keep-alive

## props

include - 字符串或正则表达，只有匹配的组件会被缓存
exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存

## 原理

在 **created 函数调用时将需要缓存的 VNode 节点保存在 this.cache 中**；在 render（页面渲染） 时，如果 VNode 的 name 符合缓存条件（可以用 include 以及 exclude 控制），则会从 this.cache 中取出之前缓存的 VNode 实例进行渲染。

# 元信息

## 配置title

```js
{
    path:"/test",
    name:"test",
    component:()=>import("@/components/test"),
    meta:{
        title:"测试页面", //配置title
        keepAlive: true //是否缓存
    }
}
```

```js
//main.js中的代码
router.beforeEach((to,from,next)=>{
    if(to.meta.title){
        document.title=to.meta.title
    }
    next()
})
```



## 是否需要登录信息

## 是否要缓存

```js
<!-- app.vue中的代码 -->
<!-- 需要被缓存的路由入口 -->
<keep-alive>  
    <router-view v-if="$route.meta.keepAlive"></router-view>
</keep-alive>

<!-- 不需要被缓存的路由入口 -->
<router-view v-if="!$route.meta.keepAlive"></router-view>
```

