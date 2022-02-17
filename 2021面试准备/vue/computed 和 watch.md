`computed` 是计算一个新的属性，并将该属性挂载到 vm（Vue 实例）上，而 `watch` 是监听已经存在且已挂载到 `vm` 上的数据，所以用 `watch` 同样可以监听 `computed` 计算属性的变化（其它还有 `data`、`props`）

`computed` 本质是一个**惰性求值的观察者**，具有缓存性，**只有当依赖变化后，第一次访问  `computed`  属性，才会计算新的值**，而 `watch` 则是当数据发生变化便会调用执行函数（ps:<span style="color:red">就是当依赖变化时，computed函数并不执行，当取这个computed的时候才执行，而watch会立即执行</span>）

computed支持缓存，有一个dirty属性 只有当依赖变化的时候，触发依赖的set 把computed的watcher设置为true 这是返回值会重新执行computed再进行返回。

从使用场景上说，**`computed` 适用一个数据被多个数据影响，而 `watch` 适用一个数据影响多个数据；**

**watch 支持异步操作**



# computed原理

computed内部实现了一个惰性的watcher，在实例化的时候不会去求值，其内部通过dirty属性标记计算属性是否需要重新求值。当computed依赖的任一状态（不一定是return中的）发生变化，都会通知这个惰性watcher，让它把dirty属性设置为true。所以，当再次读取这个计算属性的时候，就会重新去求值。





**计算属性computed :** 

\1. 支持缓存，只有依赖数据发生改变，才会重新进行计算

\2. 不支持异步，当computed内有异步操作时无效，无法监听数据的变化

3.computed 属性值会默认走缓存，计算属性是基于它们的响应式依赖进行缓存的，也就是基于data中声明过或者父组件传递的props中的数据通过计算得到的值

\4. 如果一个属性是由其他属性计算而来的，这个属性依赖其他属性，是一个多对一或者一对一，一般用computed

5.如果computed属性属性值是函数，那么默认会走get方法；函数的返回值就是属性的属性值；在computed中的，属性都有一个get和一个set方法，当数据变化时，调用set方法。

**侦听属性watch：**

\1. 不支持缓存，数据变，直接会触发相应的操作；

2.watch支持异步；

3.监听的函数接收两个参数，第一个参数是最新的值；第二个参数是输入之前的值；

\4. 当一个属性发生变化时，需要执行对应的操作；一对多；

\5. 监听数据必须是data中声明过或者父组件传递过来的props中的数据，当数据变化时，触发其他操作，函数有两个参数，

　　immediate：组件加载立即触发回调函数执行，确认是否以当前的初始值执行handler的函数。

　　deep: 深度监听，为了发现**对象内部值**的变化，复杂类型的数据时使用，例如数组中的对象内容的改变，注意监听数组的变动不需要这么做。注意：deep无法监听到数组的变动和对象的新增，参考vue数组变异,只有以响应式的方式触发才会被监听到。



```js
data(){
      return{
        'first':{
          second:0
        }
      }
    },
    watch:{
      secondChange:{
        handler(oldVal,newVal){
          console.log(oldVal)
          console.log(newVal)
        },
        deep:true
      }
    },
```