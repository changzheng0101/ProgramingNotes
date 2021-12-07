# Vue

## 常见使用

| 符号                         | 含义                                                     |
| ---------------------------- | -------------------------------------------------------- |
| {{}}                         | 解析为js                                                 |
| v-html                       | 数据被解析为html                                         |
| v-if                         | if语句                                                   |
| v-bind:属性                  | 响应式更新某个属性                                       |
| v-on:click                   | 后加事件，代表监听事件                                   |
| v-bind:[attributeName]="url" | 在指令参数中使用 JavaScript 表达式，方法是用方括号括起来 |
|                              |                                                          |
|                              |                                                          |

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







