# 渲染流程和更新流程图

![image-20210216222041313](D:\project\notebook\react\13react的更新流程.assets\image-20210216222041313.png)

# diff算法的要点

### diff是对比两个dom树，同层对比





### 当同层DOM类型不一样的时候，直接将该DOM子树干掉，render生成一个新的子树，其内部的所有都无法复用

这时候，会调用生命周期componentWillUnmount 





### 当同层dom类型相同，属性不同，只会修改属性，内部可以服用

不会componentWillUnmount 



# 子节点遍历的keys问题

#### diff算法中有两种情况

- 默认情况是依次遍历，如果是前面全部一样，最后一条有变化，则复制变化插入原来的dom

  ![image-20210216223108437](D:\project\notebook\react\13react的更新流程.assets\image-20210216223108437.png)

- 如果是在最前面插入一条数据，则会对每一个子dom发生更改不会复用，产生性能问题，所以引入keys优化

  ![image-20210216223157810](D:\project\notebook\react\13react的更新流程.assets\image-20210216223157810.png)

#### keys的优化

将循环加入一个key的时候，对于上述的情况一没有什么作用，但是对于情况二，react会根据key来替换不同的dom来达到复用的效果

#### key的要求

- key唯一
- key不要用随机数（下次render的时候会生成一个新的）
- 不要用index，对性能是没有优化

# render函数的调用

- 所有组件被创建的时候都会被调用一次
- setState时render调用

### SCU优化

shouldComponentUpdate（）生命周期控制render函数调用与否

```js
 shouldComponentUpdate(nextProps, nextState, nextContext) {
    if(nextState.counter !== this.state.counter){
      return true
    }
    return false
  }
```



当setState更改一些无关紧要的数据时（在页面上无显示）也会触发render函数

通过SCU优化来控制render的调用

demo 只有在counter改变的时候才会调用render

```js
import React, {Component} from 'react';

class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      message:'hello',
      counter:0
    }
  }



  render() {
    console.log('render')
    return (
        <div>
          <h2>{this.state.counter}</h2>
          <button onClick={e => this.btnClick()}>+1</button>
          <button onClick={e => this.changeMessage()}>change</button>
        </div>
    );
  }

  shouldComponentUpdate(nextProps, nextState, nextContext) {
    if(nextState.counter !== this.state.counter){
      return true
    }
    return false
  }

  btnClick(){
    this.setState({
      counter:this.state.counter+1
    })
  }
  changeMessage(){
    this.setState({
      message:'11111'
    })
  }
}

export default App;

```

### PureComponent

在SCU优化的时候如果数据量太大，比较过于麻烦，类组件可以直接继承PureComponent，当state发生改变的时候，会对state进行浅层比较来防止render函数的过多调用。

##### 缺陷：无法阻止函数组件的render调用

## memo 的使用

- 使用

  ```js
  import {memo} from 'react'
  
  const memoHeader = memo(function Header(){
      return(
          <div>我头</div>
      )
  })
  
  <memoHeader/>
  ```

  

这样react也会对这个函数组件进行state优化，没有修改时不会调用他的render函数