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
 















