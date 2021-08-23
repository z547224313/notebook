名称：命令行变元数组

内容：**传的参数**+**node.exe绝对路径**+**node所执行文件的绝对路径**

其中传的参数就是 npm i -dev -a -b 



```js
// 文件p1.js中
console.log(process.argv);

>>>命令行中输入
node p1.js --a -b c

<<< 输出
E:\w>node p1.js --a -b c
[ 'C:\\Program Files\\nodejs\\node.exe',
  'E:\\w\\p1.js',
  '--a',
  '-b',
  'c' ] 
  

```

