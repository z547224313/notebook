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

