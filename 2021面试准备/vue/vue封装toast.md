```js
想用插件vue,use调用，就要在这个组件的文件夹下面创建一个index.js
import Toast from "@/components/common/toast/Toast";

const obj={}

obj.install=function (Vue) {
  //main.js中使用Vue.use(插件名)
  //就会调用该函数
  //1.创建组件构造器

  const toastConstructor = Vue.extend(Toast)
  //2.用new的方式，根据组件构造器创建一个组件对象
  const toast = new toastConstructor()
  //3.讲组件对象，手动挂载到某一个元素上
  toast.$mount(document.createElement('div'))
  //4.加到body上
  document.body.appendChild(toast.$el)
  console.log(toast);

  Vue.prototype.$toast = toast
  //最终挂载元素，插件封装完成

}
```

