Vue 实现响应式并不是数据发生变化之后 DOM 立即变化，而是按一定的策略进行 DOM 的更新。

$nextTick 是在下次 DOM 更新循环结束之后执行延迟回调，在修改数据之后使用 $nextTick，则可以在回调中获取更新后的 DOM，API 文档中官方示例如下：

```js
new Vue({
  // ...
  methods: {
    // ...
    example: function () {
      // modify data
      this.message = 'changed'
      // DOM is not updated yet
      this.$nextTick(function () {
        // DOM is now updated
        // `this` is bound to the current instance
        this.doSomethingElse()
      })
    }
  }
})
```