# Vue-Notes

## Vue实例

### 如何使用Vue实例

**方法一：从HTML得到试图**

* Vue文档中所说的完整版Vue
* 从CDN引用vue.js或vue.min.js
* 通过import引用vue.js或者vue.min.js

**方法二：用JS构建试图**

使用文档链接

**方法三：使用vue-loader**

使用.vue文件翻译成h构建方法


### Vue实例的作用

**Vue实例就如同jQuery实例**

封装了对DOM的所有操作；</br>
封装了对data的所有操作；</br>


**操作DOM：**

监听事件、改变DOM

**操作data**

增删改查

### Vue完整版和runtime的区别：

**Vue完整版**

Vue完整版同时包含编译器和运行时的版本；</br>
编译器：用来将模板字符串编译成为JavaScript渲染函数的代码；</br>
运行时：用来创建Vue实例、渲染并处理虚拟DOM等的代码。

**runtime版**

不含编译器。只包含运行时的版本

**两个版本的区别**

|     | Vue完整版  | Vue runtime版  |
|  ----  | ----  |  ----  |
| 特点  | 有编译器 | 无编译器 |
| 试图  | 直接写在HTML里，或用template渲染到HTML | 利用render里的h函数来创建HTML节点 |
| cdn 引入  | https://cdn.bootcss.com/vue/2.6.10/vue.min.js | https://cdn.bootcss.com/vue/2.6.10/vue.runtime.min.js |
| webpack引入  | 需要配置alias | 默认使用此版本 |
| @vue/cli 引入  | 需要额外配置 | 默认使用此版本 |

**两者的使用场景**

*  Vue完整版虽然有编译器，可以直接操作HTML节点，但是它的体积相对于runtime版本多出40%，所以完整版更适用于开发环境`

* Vue runtime版抛弃了编译器，体积小了很多，适应于生产版本

## Vue中的options

**options的五类属性**

* 数据：data、props、propsData、computed、methods、watch

* DOM: el、template、render、renderError;

* 生命周期钩子：beforeCreate、created、beforeMount、mounted、beforeUpdate、updated、activated、deactivated、beforeDestory、destoryed、errorCaptured;

* 资源：directives、filters、components;

* 组合：parent、mixins、extends、provide、inject;

**基本属性**

* el-挂载点：可以用$mount代替
* data-内部数据：支持对象和函数，优先用函数
* methods-方法：事件处理函数或者是普通函数
* components:Vue组件，注意大小写
* 四个钩子：</br>
  created-实例出现在内存中；</br>
  mounted-实例出现在页面中；</br>
  updated-实力更新；</br>
  destoryed-实例从页面和内存中消亡;</br>
* props-外部数据/属性：</br>
  message="n"传入字符串；</br>
  :message="n"传入this.n数据；</br>
  :fn-"add"传入this.add函数</br>
  
### Vue数据响应式

**Object.defineProperty**

* 可以给对象添加属性value
* 可以给对象添加gette / setter
* getter / setter用于对属性的读写进行监控

**设计模式（代理）**

对myData对象的属性读写，全权由另一个对象vm负责，那么vm就是myData的代理。

**vm = new Vue({data:myData})**


### 数据响应式

响应式：对外界操作做出反应成为响应式

**Vue的data是响应式**

**Vue.set和this.$set**

* 作用：</br>
  新增key;</br>
  自动创建代理和监听；</br>
  触发UI更新;</br>

`举例：this.$set(this.object,'m',100
)`

**总结：**

* 对象中新增的key</br>
  Vue无法事先监听和代理；</br>
  使用set来新增key，创建监听和代理，更新UI，需要提前把属性都写出来；</br>

* 数组中新增的key</br>
  数组新增key最好通过7个API；
  
## Computed和Watch

### option中的进阶属性

* Computed-计算属性</br>
  无需加括号；</br>
  根据依赖是否变化来缓存；</br>
  
* Watch-侦听</br>
  一旦data变化，就执行函数；</br>
  options.watch;</br>
  this.$watch用法；</br>
  deep,immeditate含义；</br>
  
* directives-指令 </br>
  内置指令v-if/v-for/v-bind/v-on;</br>
  自定义指令，如v-focus;</br>
  指令是为了减少重复的DOM操作；</br>
  
* mixin-混入</br>
  重复三次之后的出路；</br>
  混入v.s.全局混入；</br>
  选项自动合并；</br>
  混入就是为了减少重复的构造选项；</br>
  
* extends-继承</br>
  继承是为了减少重复的构造选项；</br>
  
* provide/inject 

**响应式原理**

* options.data</br>
  会被Vue监听；</br>
  会被Vue实例代理；</br>
  每次对data的读写都会被Vue监控；</br>
  Vue会在data变化时更新UI；</br>
  

### Computed

* 用途：</br>
  被计算出来的属性就是计算属性</br>

* 缓存：</br>
  如果依赖的属性没有变化，就不会重新计算，getter/setter默认不会做缓存，Vuez做了特殊处理
  

### Watch

* 用途：</br>
  当数据变化时，执行一个函数

* 语法：<a href="https://cn.vuejs.org/v2/api/#watch">推荐看文档</a>

### watch和computed的区别
computed(计算属性)-watch(监听)</br>

computed看上去是方法，但是实际上是计算属性，该属性用来计算出一个值(就是你所依赖的数据动态显示的计算结果，该计算结果会被缓存)。commputed的值在getter执行后是会缓存的，只有在它以来的属性值改变之后，下一次获取computed的值才会重新调用相应的getter来计算。</br>

该值在调用的时候不需要加括号，可以作为属性直接使用。二是根据依赖自动缓存，如果依赖不变那么computed的值不会发生变化</br>

watch用来监听data的数据回调，当依赖的data的数据发生变化时执行回调。在方法中传入newVal和oldVal，可以提供输入值无效，提供中间值的场景。Vue实例会在实例化时调用$watch(),遍历watch对象的每一个属性。</br>

watch有两个选项：immeditate表示是否在第一次渲染的时候执行该函数，第二个选项是deep,deep的作用是在渲染的时候是否去监听属性的变化。</br>

总结:
1:如果一个数据依赖于其他数据，那么就把这个数据设计为computed的</br>
2:如果需要在某个数据变化时做一些事情，使用watch来观察这个数据变化


### Vue模板

**模板template三种写法**

```
一：Vue完整版，写在HTML里
<div id=xxx>
   {{n}}
   <button @click="add">+1</button>
</div>

new Vue({
   el: '#xxx',
   data:{n:0},// data可以改成函数
   methods:{add()}
})
```
```
二：Vue完整版，写在选项里

<div id=app>
</div>

new Vue({
  template:`
     <div>
        {{n}}
        <button @click="add">+1</button>`
   data:{n:0},//data可以改成函数
   methods:{add(){ this.n += 1}}
}).$mount('#app')
// 细节：div#app 会被替代
  
```

```
三、Vue非完整版，配合xxx.vue文件

<template>
   <div>
     {{n}}
     <button @click="add">
        +1
     </button>
     </div>
</template>


<script>
export default { 
  data(){ return {n:0} },
  // data必须为函数
  methods:{add(){this.n += 1}}
}
</script>
<style>此处为CSS</style>

在另一个文件中写下：
import Xxx from './xxx.vue'
// Xxx是一个options对象
new Vue({
   render: h => h(Xxx)
}).$mount('#app')

```

### Vue模板中的语法

**表达式**

* {{ object.a}}表达式
* {{ n + 1 }}可以写任何运算
* {{ fn(n) }}可以调用函数
* 如果值为undefined 或 null就不显示
* <div v-text="表达式"></div>

**HTML内容**
* 假设data.x值为`<strong>hi</strong>`
* `<div v-html="x"></div>`即可显示粗体的hi

**绑定属性**

* 绑定src
`<img v-bind:src="x" />`

* v-bind:简写为:
`<img :src="x" />`

* 绑定对象
```
<div 
:style="{border: '1px solid red',height:100}>
//此处把'100px'写成100

</div>
```

**绑定事件**

* v-on:事件名
```
<button v-on:clcik="add">+1</button>
//点击之后，Vue会运行add()

<button v-on:click="xxx(1)">xxx</button>
//点击之后，Vue会运行xxx(1)

<button v-on:click="n+=1">xxx</button>
//点击之后，Vue会运行n+=1;
```

* 缩写
`<button @click="add">+1</button>`


**条件判断**

* if...else
```
<div v-if="x>0">
x大于0
</div>

<div v-else=if="x===0">
x为0
</div>

<div v-else>
x小于0
</div>

```

**循环**

* for(value,key)in对象或数组
```
<ul>
   <li v-for="(u,index) in users" :key="index">
      索引：{{index}} 值： {{u.name}}
   </li>
</ul>

<ul>
   <li v-for="(value,name) in obj" :key="name">
     属性名：{{name}},属性值：{{name}}
    </li>
 </ul>
 
```

**显示、隐藏**

* v-show
`<div v-show="n%2===0">n 是偶数</div>`

* 近似等于 

`<div :style="{display:n%2===0?'block':'none'}">n 是偶数 </div>`

看得见的元素display不只有block，如table的display为table,li的display为list-item

**总结**

* Vue模板主要特点有：</br>
 使用XML语法（不是HTML）；</br>
 使用{{}}插入表达式；</br>
 使用v-html v-on v-bind 等指令操作DOM；</br>
 使用v-if v-for等指令实现条件判断和循环；</br>
 
 
### 指令Directive

**指令**

* 什么是指令？
```
<div v-text="x"></div>
<div v-html="x"></div>

以v-开头的东西就是指令
```

* 语法</br>
v-指令名：参数=值，如v-on:click=add;</br>
如果值里没有特殊字符，则可以不加引号；</br>
有些指令没有参数和值；</br>
有些指令没有值，如v-on:click.prevent;</br>

**修饰符**

* 有些指令支持修饰符</br>
@click.stop="add"表示阻止事件传播/冒泡；</br>
@click.prevent="add"表示阻止默认动作；</br>
@click.stop.prevent="add"同时表示两种意思；</br>

* 一共有多少修饰符呢？
v-on支持的有.{keycode | keyAlias}
.stop.prevent.capture.self.once.passive.native;
快捷键相关.ctrl.alt.shift.meta.exact;
鼠标相关：.left.right.middle;
v-bind支持的有.prop.camel.sync;
v-model支持的有.lay.number.trim

**.sync修饰符**

* Vue规则:组件不能修改props外部属性

* Vue规则：this.$emit可以触发事件，并传参；

* Vue规则：$event可以获取$emit的参数

### 总结

**@click.stop="xxx"**

**@click.prevent="xxx"**

**@keypress.enter="xxx"**

**:money.sync="total"**

### Directives

**两种写法**

· 一、声明一个全局指令

`Vue.directive('x',directiveOptions)`这样就可以在任何组件里用v-x;

·二、声明一个局部指令
```
new Vue({
  ...,
  directives: {
     "x":directiveOptions
  }
 })
```
**directiveOptions**

* 五个函数属性
```
bind(el,info,vnode,oldVnode)-类似created
inserted(el,info,vnode,oldVnode）-类似mounted
update(el,info,vnode,oldVnode)-类似updated
componentUpdated(el,info,vnode,oldVnode)
unbind(el,info,vnode,oldVnode)-类似destoryed
```

**指令的作用**

* 主要用于DOM操作
Vue实例/组件用于数据绑定、事件监听、DOM更新；</br>
Vue指令主要目的就是原生DOM操作；

* 减少重复
如果某个DOM操作你经常使用，就可以封装为指令；</br>
如果某个DOM操作比较复杂，也可以封装为指令；</br>

### mixins-混入

混入就是复制；

**减少重复**

* 类比
directives的作用是减少DOM操作的重复；</br>
mixins的作用是减少data、methods、钩子的重复；

**mixins技巧**

<a href="https://cn.vuejs.org/v2/guide/mixins.html#%E9%80%89%E9%A1%B9%E5%90%88%E5%B9%B6">选项只能合并</a>

### extends-继承

extends是比mixins更抽象一点的封装；

### provide和inject-提供和注入

**总结：**</br>
作用：大范围的data和method等共用；</br>
注意：不能只传themeName不传changeTheme,因为themeName的值是被复制给provide的；

### 总结：

**directives指令**</br>
全局用Vue.directive('x',{...});</br>
局部用options.directives;</br>
作用是减少DOM操作相关重复代码;</br>

**mixins混入**</br>
全局用Vue.mixin({...});</br>
局部用options.mixins:[mixin1,mixin2];</br>
作用是减少options里的重复；</br>

**extends继承/扩展**</br>
全局用Vue.extend({...});</br>
局部用options.extends:{...};</br>
作用跟mixins差不多，只是形式不同；</br>

**provide/inject提供和注入**</br>
祖先提供东西，后代注入东西；</br>
作用是大范围、隔N代共享信息；</br>








































