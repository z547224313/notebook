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

