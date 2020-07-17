## 导出

```javascript
module.exports.c = {}
```

以上只导出一个对象

```javascript
exports.c=c
exports.add=(a,b)=>a+b
```

 以上可以导出多个

## 导入

```javascript
let c = require('./文件名.js')
```

<span style='color:red'>没有带有路径，引用的是当前文件所在当前目录下的node_modules目录下的模块。</span>

commonjs引用模块只在第一次被使用时执行一次<span style='color:red'>是值得拷贝</span>

 