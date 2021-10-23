Vuex本质是一个对象

Vuex对象有两个属性，一个是install方法，一个是Store这个类

install方法的作用是将store这个实例挂载到所有的组件上，注意是同一个store实例。

Store这个类拥有commit，dispatch这些方法，Store类里将用户传入的state包装成data，作为new Vue的参数，从而实现了state 值的响应式。





这也就解释了为什么store中的对象需要先定义好才能完成双向绑定



# 

```js
class Store{

    constructor(options) {
        this.vm = new Vue({
            data:{
                state:options.state // 放入vm中直接进行双向绑定
            }
        })
      //vuex的get方法
			 let getters = options.getter || {}
        this.getters = {}
        Object.keys(getters).forEach(getterName=>{
            Object.defineProperty(this.getters,getterName,{
                get:()=>{
                    return getters[getterName](this.state)//这里就是取属性，所以getter方法不用写括号
                }
            })
        })
      
     	//mutation
      let mutations = options.mutations || {}
        this.mutations = {}
        Object.keys(mutations).forEach(mutationName=>{
            this.mutations[mutationName] =  (arg)=> {
                mutations[mutationName](this.state,arg)
            }
        })
      
      //action
      let actions = options.actions
        this.actions = {}
        Object.keys(actions).forEach(actionName=>{
            this.actions[actionName] = (arg)=>{
                actions[actionName](this,arg) //注意这里传入的是this 整个Stroe实例，因为我们在action中要调用commit
            }
        })

      	
		// end constructor
    }
  
    //保证可以直接 this.$store.state拿到state
    get state(){
        return this.vm.state
    }
  	//commit 出发this.mutation的方法 因为action中异步调用commit，所以要用箭头函数修改this指向问题
  	commit=(method,arg)=>{
        console.log(method);
        console.log(this.mutations);
        this.mutations[method](arg)
    }

  	dispatch(method,arg){
        this.actions[method](arg)
    }


}

```

