# Vue

## 视频任务

* {{}}

* v-bind 使用

* mount决定挂载在哪里

* methods 

* 在html中调用js中的方法

* 方法中访问data中的数据

* 一个训练

* 给button添加响应事件 

* 给响应函数添加参数

* input中的值显示到p中

* 响应函数默认有event参数

* $event的使用

* 阻止默认的事件行为，form的提交会刷新整个网页，vue可以按需刷新
  * 在方法中对事件进行处理，不让其继续流动
  * 给监听事件添加修饰，对齐进行限制
  
* v-bind 数据单向流动，从js流动到组件

*  每当页面需要有部分重新渲染的时候，vue中执行的方法也会都执行，因为vue不知道这个方法是否用到了你改变的数据。

* 计算属性，知道用到data中的哪个数据，这样只有data中数据更新时候，对应的才会更新，按需更新，**computed**

  * ```
    computed:{
    	fullname(){
    		return name + "some thing"
    	}
    }
    ```

  * 使用时候fullname，不用加括号调用  

* watch

  * 用于当某些值**变化**的时候响应，也可以观察计算属性

  * ```
    watch:{
    	name(value){
    	
    	}
    }
    ```

  * name是改变的属性的名字，value是当前name属性对应的值

* setTimeout 中得用that保存this

* 给不同的状态绑定属性

  * ```
    :style="{borderColor: selected?'red':'#ccc'}"
    ```

  * inline方式会覆盖别的属性，不常用

  * ```javascript
    :class="{styleA:boolean,styleB:boolean}"
    ```

  * 能将:class绑定到computed value，将逻辑分离

* v-if v-else v-else-if

* v-for

  * ```javascript
    goal in goals
    ```

  * 注意使用in

  * ```javascript
    (goal,index) in goals
    ```

  * ```javascript
    (key,value) in {name:"ben",age:31}
    ```

  * ```javascript
    (key,value,index) in {name:"ben",age:31}
    ```

  *   当列表数量改变的时候，每一项是按需加载，尽量会复用之前的,第一项和第二项都有个input，当删除第一项之后，假设第 一项的input 有值，这个input中的值还是会被保存下来。当往第二个input中输入一些东西的时候，删除第一个，第二个中的input会被删除，复用了第一个的input

  * 用:key = "something unique"可以改善上面的那种情况，**不能用index**，其实就是用一个key对应一个项目，这样不同的项目之间组件不会混用，如果用index，index是会发生改变的
  
* 在自己的组件中使用v-model

  * props:['modelValue']
  * emits:['update:modelValue']
  * v-model仅仅是一个简写

## 常见使用

| 符号                         | 含义                                                     |
| ---------------------------- | -------------------------------------------------------- |
| {{}}                         | 解析为js                                                 |
| v-html                       | 通常是字符串，数据被解析为html，和属性一样               |
| v-if v-else v-else-if        | if语句,else的元素需要直接更在if元素之后，直接删除DOM元素 |
| v-bind:属性                  | 响应式更新某个属性                                       |
| v-on:click                   | 后加事件，代表监听事件                                   |
| v-bind:[attributeName]="url" | 在指令参数中使用 JavaScript 表达式，方法是用方括号括起来 |
| v-model                      | v-bind:value + v-on:input 完成数据的双向绑定             |
| v-show                       | 设置display为none来隐藏元素                              |

![image-20220512134416060](../../md_img/Vue/image-20220512134416060.png)

![image-20220512153026708](../../md_img/Vue/image-20220512153026708.png)

## 缩写 

### `v-bind` 缩写

```html
<!-- 完整语法 -->
<a v-bind:href="url"> ... </a>

<!-- 缩写 -->
<a :href="url"> ... </a>

<!-- 动态参数的缩写 -->
<a :[key]="url"> ... </a>
```

### `v-on` 缩写

```html
<!-- 完整语法 -->
<a v-on:click="doSomething"> ... </a>

<!-- 缩写 -->
<a @click="doSomething"> ... </a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```

## 注意

小写强制转化

```html
<!--
在 DOM 中使用模板时这段代码会被转换为 `v-bind:[someattr]`。
除非在实例中有一个名为“someattr”的 property，否则代码不会工作。
-->
<a v-bind:[someAttr]="value"> ... </a>
```

this关键字指向该组件实例，使用匿名函数的时候应该注意

## 函数防抖和节流

###### 防抖（debounce）

**所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。**

###### 节流（throttle）

**所谓节流，就是指连续触发事件但是在 n 秒中只执行一次函数。**

## 计算属性

可以理解为默认的get方法,使用时候和函数不同，不用加括号，意味着再次执行的时候，不用重新进行计算，**计算属性是基于它们的响应依赖关系缓存的**

声明在**computed**中

<div id="computed-basics" class="demo">
  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>
</div>

```javascript
Vue.createApp({
  data() {
    return {
      author: {
        name: 'John Doe',
        books: ['Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery']
      }
    }
  },
  computed: {
    // a computed getter
    publishedBooksMessage() {
      // `this` points to the vm instance
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  }
}).mount('#computed-basics')
```

## watch 侦听器

使用 `watch` 选项允许我们执行异步操作 (访问一个 API)，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。



## v-if  v-show

`v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好



## v-model

用于和其他属性完成双向绑定

## proxy

```javascript
// proxy
const data = {
    message: "hello",
    longMessage: "hello world"
}

const handler = {
    set(target, key, value) {
        //target 是目前的值 key是修改的key  value是修改的value
        if (key === "message") {
            target.longMessage = value + " world";
        }
        target.message = value;
    }
}


const proxy = new Proxy(data, handler);

// 修改之后自动触发set方法
proxy.message = "something";

// 如果target.message不改，则data中的数据不会发生改变
console.log(data);
```

## template

>就是将创建的app挂载到到哪个html下了，那部分html就是templat

## refs

```javascript
<input ref="inputText"/>

//获得JavaScript对象
this.$refs.inputText
```





## 如何更新DOM

渲染页面的时候，会将vue的指令给消除，换成普通的html，当vue中有值更新的时候，不会遍历整个DOM，找到需要更新的DOM，这种性能会很差，和重新渲染差不多，Vue的解决办法是使用一种**虚拟DOM**，每当有数据改变的时候，更新虚拟DOM，然后和之前的虚拟DOM对比，然后再反应到真实的DOM

![image-20220512180045134](../../md_img/Vue/image-20220512180045134.png)

## Vue声明周期

![image-20220512180841596](../../md_img/Vue/image-20220512180841596.png)

## component

```javascript
const app = Vue.createApp({
    //something
});
app.component("friend-component",{
	//和普通创建的对象一样
}); 
app.mount("#test");
```

```html
<friend-component></friend-component>  
```

### global&Local

在main.js中注册就是global的，一开始加载的时候，组件就会加载，local是在每个vue文件中定义的，只有定义了local组件的vue文件可以用该组件，local也是按需加载的。

## provide&inject

有时候数据会顺着很底层的组件流动到父组件，需要流动好几层，这时候可以选择在父组件中provide，之后在子组件中进行inject，这种使用必须有父子关系，**邻居关系无法工作**，也可以provide函数，然后inject到别的组件中，可以代替事件的向上传播，可以让组件直接执行想执行的函数，**该方法只有在跨越多个组件传播时才使用**，如果只是一个组件，还是通过props和emit事件来进行通信，代码可读性更高。

```javascript
// parent
provide(){
	return {
        topics:this.topics
    }
}

//child
inject:['topics']
```

![image-20220513100955760](../../md_img/Vue/image-20220513100955760.png)

## slots

在组件中使用，外界可以通过slot往这个组件中注入html代码

`$slots`可以访问所有的slot

```html
<!-- 组件内 -->
<!-- 有header才渲染这个slot -->
<header v-if="$slots.header">
	<slot name = "header">
	</slot>
</header>
<slot></slot>

```

```html
<component-name>
	<template #header>
		//
	</tempalte>
	<template #default>
		//
	</tempalte>
</component-name>

Or


<component-name>
    // html code
</component-name>
```

## 动态组件

将someValue对应的组件渲染出来，上面的表述和下面的表述相同

```html
<component :is="someValue"></component>

<someValue></someValue>
```

组件切换之后不会重新渲染丢失数据

```html
<keep-alive>
    <component :is="someValue"></component>
</keep-alive>
```

将html换一个地方渲染，更加具有意义，一般多使用于弹窗等。

```html
<teleport to="body">
    //html code
</teleport>
```

![image-20220513135408260](../../md_img/Vue/image-20220513135408260.png)

如果自定义组件中的html元素中没有某个属性，这个属性会自动降落到组件中，落到组件的根元素上，这是vue的特性。

provide和inject，当二者指向同一个引用的时候，更改可以同步更新，当provide中的对象被覆盖之后，inject中的对象无法完成更新。也就是inject还是参考的原来的对象。

## 向后端申请数据

1. fetch

   1. ```javascript
      fetch('url',{
      	method:"POST",
      	headers:{
      		'Content-type':'application/json'
      	},
      	body:JSON.stringify({
      		// json object
      	})
      })
      ```

   2. ```javascript
      //fetch请求默认为get请求，会返回一个Promise对象
      fetch('url').then((response)=>{
      	//dosomething
      })
      ```

   3. ```javascript
      ()=>{} //里面的this和外面的this是同一个this
      function() {} //里面的this和外面的this不是同一个，访问会出错
      ```

   4. 显示loading通过添加属性来显示加载过程

   5. ```javascript
      fetch('url').then((response)=>{
      	//dosomething
      })
      .catch((error)=>{}) //deal error
      ```

   6. 

2. axios

## Router

```bash
npm install --save vue-router@next
```

在main.js中定义路由

```javascript
const route = [
    xxx
]

const router = createRouter({
	history : createWebHashHistory(),
	routes
})


app.use(router)
	.mount("#app");
```

使用视图

```html
<router-view></router-view> 
```



```
this.$router.push('url')
this.$route.params.xxx
```

```
<router-link to=""></router-link>
```

当更新组件的时候，如果/team/:teamId 仅仅是`teamId`改变了，并不会重新构建这个对象，如果想要进行更新，要watch`$route`的变化 

```javascript
{path:"/team/:teamId",component:xxxx,props: true}
//teamId 会和props一样传入
//在组件中可以通过props来读取teamId
```

  children的作用，相当于在一个组件中嵌套另一个组件，需要在有children的那个组件中添加`<router-view></router-view> `作为路由出口。

## animation

用`<transtion>`包裹想要有动画的元素，**且只能有一个直接的child**，注意是渲染之后的，不是里面只有一个组件，假如里面有一个自定义组件，自定义组件里面还有别的组件，这种情况下是无法正常工作的，下面的这些css会在动画结束之后被移除

```css
//add
// start state
.v-enter-form{

}
.v-enter-active{
	transition: all .3s; //需要添加持续时间
}
// end state
.v-enter-to{

}

//delete
// start state
.v-leave-form{

}
.v-leave-active{
	animation: animation-name .3s;
}
// end state
.v-leave-to{

}
```

有多个transtion，每个transition想要不同的动画

```html
<transtion name="some"></transtion>
```

css属性变为

```css
//add
// start state
.some-enter-form{

}
.some-enter-active{
	transition: all .3s; //需要添加持续时间
}
// end state
.some-enter-to{

}

//delete
// start state
.some-leave-form{

}
.some-leave-active{
	animation: animation-name .3s;
}
// end state
.some-leave-to{

}
```

也就是说默认为v，其他情况下根据name来

另一种方式，enter-active-class也可以和其他几个属性结合使用

```html
<transtion enter-active-class="name"></transtion>
```

可以添加多个组件的情况：在transtion包裹的条件下，多个组件只会同时显示一个

可以监听transition的进入和删除DOM事件

为一个列表定义动画

```html
<transition-group tag="ul" name="user-list">
	<li></li>
</transition-group>
```

## Vuex

### 作用

管理数据，替代provide和inject完成多个组件之间数据共享，用于管理全局数据

![image-20220515211715063](../../md_img/Vue/image-20220515211715063.png)

将数据和修改放到一起，在组件中进行调用

![image-20220516144805888](../../md_img/Vue/image-20220516144805888.png)

```javascript
 const store = createStore({
 	state(){
 		return {
 			//xxxx
 		}
 	},
 	mutations:{
 		//methods
 	},
    getters:{
        //methods
        methodsName(state){
            return state.xxx;
        }
    },
    actions:{
        //可以添加耗时操作
    }
 })
```

```javascript
this.$store.commit('mutation name')
this.$store.dispatch('action name')
this.$store.getter['property']
```

![image-20220516145411628](../../md_img/Vue/image-20220516145411628.png)

![image-20220516150034604](../../md_img/Vue/image-20220516150034604.png)

一个程序一般有一个store，但是一个stroe可以整合多个module，可以为不同的module提供不同的namespace，调用的时候也要和不同的namespace结合在一起。

action可以通过context访问全局的所有变量，而在motations中定义的方法，只能访问state，也就是一个module中的变量。