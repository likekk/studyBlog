> 寄语：每个人都有彷徨的时候，彷徨并不可怕，可怕的是在彷徨中不断的做抉择。因为一旦有了抉择，就不会再彷徨，就会按照既定的方向去行事。																																						摘自《超兽武装》

> 本文已收录至[https://github.com/likekk/-Blog](https://github.com/likekk/-Blog)欢迎大家star :smile::smile: :smile: ,共同学习，共同进步。如果文章有错误的地方，欢迎大家指出。后期将在将GitHub上规划前端学习的路线和资源分享。



### 写在前面

每一篇文章都希望您有所收获，每一篇文章都希望您能静下心来浏览、阅读。每一篇文章都是作者精心打磨的作品。

【**原创不易、请勿白嫖**】。如果您觉得二郎神杨戬有点东西的话，作者希望你可以帮我点亮那个点赞的按钮，对于二郎神杨戬这个暖男来说，**真的真的非常重要**，这将是我持续写作的动力。您只需要小手轻轻一点，带来的却是温暖了这个作者，给予他前进的动力。

​																																										——致读者们

### 前言

通过上一篇博客的学习，我们初步入门了Vue.js这个渐进式框架，简单的了解了一下声明式渲染、条件与循环、处理用户输入和表单、组件应用构建等相关内容。本篇博客将会延续上一篇博客的内容进行探索Vue.js。那么一起带着一颗平静的心和二郎神杨戬一起学习吧！



### Vue实例

每个 Vue 应用都是通过用 `Vue` 函数创建一个新的 **Vue 实例**开始的：

```javascript
const vm=new Vue({
	//选项
})
```

当创建一个 Vue 实例时，你可以传入一个**选项对象**，常见的有：

- data：对象或者函数
- methods：方法，所有需要执行的方法都必须放在methods里面
- el：挂载DOM的根元素
- computed：计算属性
- Vue生命周期的钩子函数：beforeCreate、created、beforeMount、mounted、beforeUpdate、updated、activated、deactivated、beforeDestory、destoryed
- watch：监听属性



### 数据和方法

当一个 Vue 实例被创建时，它将 data对象中的所有的 property 加入到 Vue 的**响应式系统**中。当这些 property 的值发生改变时，视图将会产生**“响应”**，即匹配更新为新的值。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<div id="app">

</div>
<script src="../js/vue.js"></script>
<script>
    //  我们的数据对象
    const data={
        obj:1
    }
    //  该对象被加入到一个vue实例中
    const vm=new Vue({
        el:'#app',
        data:data
    });
    console.log(vm.obj===data.obj);
    vm.obj=10;
    console.log(data.obj);  //  10
    data.obj=100;
    console.log(vm.obj);    //  100
</script>
</body>
</html>

```

当这些数据改变时，视图会重新渲染。



**注意：**

> 只有当实例被创建时就已经存在于data中property才是响应式的，如果时创建成功之后再重新添加是无法形成响应式的。



1、添加默认初始值

如果我们后期可能需要用到某些数据、并且这些数据需要响应式的，那么我们就可以在data中先定义一些数据，并设置初始值。

```javascript
data:{
	name:'',
	age:0,
	sex:''
}
```



除了数据 property，Vue 实例还暴露了一些有用的实例 property 与方法。它们都有前缀 `$`，以便与用户定义的 property 区分开来：

```javascript
const data={
    a:1
}
const vm=new VUe({
    el:'#app',
    data:data,
});
console.log(vm.$data===data);	//	true
console.log(vm.$el===document.getElementById("#app"));

```



#### 实例属性

```javascript
vm._uid // 自增的id
vm._isVue // 标示是vue对象，避免被observe
vm._renderProxy // Proxy代理对象
vm._self // 当前vm实例

vm.＄parent // 用于自定义子组件中，指向父组件的实例
vm.＄root // 指向根vm实例
vm.＄children // 当前组件的子组件实例数组
vm.＄refs 

vm._watcher = null
vm._inactive = null
vm._directInactive = false
vm._isMounted = false // 标识是否已挂载
vm._isDestroyed = false // 标识是否已销毁
vm._isBeingDestroyed = false // 标识是否正在销毁

vm._events // 当前元素上绑定的自定义事件
vm._hasHookEvent // 标示是否有hook:开头的事件

vm.＄vnode // 当前自定义组件在父组件中的vnode，等同于vm.＄options._parentVnode
vm._vnode // 当前组件的vnode
vm._staticTrees // 当前组件模板内分析出的静态内容的render函数数组
vm.＄el // 当前组件对应的根元素

vm.＄slots // 定义在父组件中的slots，是个对象键为name，值为响应的数组
vm.＄scopedSlots = emptyObject
// 内部render函数使用的创建vnode的方法
vm._c = (a, b, c, d) => createElement(vm, a, b, c, d, false)
// 用户自定义render方法时，传入的参数
vm.＄createElement = (a, b, c, d) => createElement(vm, a, b, c, d, true)

vm._props // 被observe的存储props数据的对象
vm._data // 被observe的存储data数据的对象
vm._computedWatchers // 保存计算属性创建的watcher对象
```



#### 实例方法

```javascript
vm.$watch	//	观察 Vue 实例上的一个表达式或者一个函数计算结果的变化
vm.$set		// 向响应式对象中添加一个 property，并确保这个新 property 同样是响应式的
vm.$delete	//	删除对象的 property。如果对象是响应式的，确保删除能触发更新视图
vm.$on		//	监听当前实例上的自定义事件
vm.$once	//	监听一个自定义事件，但是只触发一次。一旦触发之后，监听器就会被移除
vm.$off		//	移除自定义事件监听器
vm.$emit	//	触发当前实例上的事件。附加参数都会传给监听器回调
vm.$mount	//	手动地挂载一个未挂载的实例
vm.$beforcepdate//	迫使 Vue 实例重新渲染
vm.$nextTick	//	将回调延迟到下次 DOM 更新循环之后执行
vm.$destory		//	
```



#### 实例参数vm.＄options

vm.＄options其实也就是我们new Vue(options)options这个选项对象可传入的属性

```javascript
declare type ComponentOptions = {
  // data
  data: Object | Function | void;  // 传入的data数据
  props?: { [key: string]: PropOptions }; // props传入的数据
  propsData?: ?Object;  // 对于自定义组件，父级通过`props`传过来的数据
  computed?: {  // 传入的计算属性
    [key: string]: Function | {
      get?: Function;
      set?: Function;
      cache?: boolean
    }
  };
  methods?: { [key: string]: Function }; // 传入的方法
  watch?: { [key: string]: Function | string };  // 传入的watch

  // DOM
  el?: string | Element;  // 传入的el字符串
  template?: string;  // 传入的模板字符串
  render: (h: () => VNode) => VNode;  // 传入的render函数
  renderError?: (h: () => VNode, err: Error) => VNode;
  staticRenderFns?: Array<() => VNode>;

  // 钩子函数
  beforeCreate?: Function;
  created?: Function;
  beforeMount?: Function;
  mounted?: Function;
  beforeUpdate?: Function;
  updated?: Function;
  activated?: Function;
  deactivated?: Function;
  beforeDestroy?: Function;
  destroyed?: Function;

  // assets
  directives?: { [key: string]: Object }; // 指令
  components?: { [key: string]: Class<Component> }; // 子组件的定义
  transitions?: { [key: string]: Object };
  filters?: { [key: string]: Function }; // 过滤器

  // context
  provide?: { [key: string | Symbol]: any } | () => { [key: string | Symbol]: any };
  inject?: { [key: string]: string | Symbol } | Array<string>;

  // component v-model customization
  model?: {
    prop?: string;
    event?: string;
  };

  // misc
  parent?: Component; // 父组件实例
  mixins?: Array<Object>; // mixins传入的数据
  name?: string; // 当前的组件名
  extends?: Class<Component> | Object; // extends传入的数据
  delimiters?: [string, string]; // 模板分隔符

  // 私有属性，均为内部创建自定义组件的对象时使用
  _isComponent?: true;  // 是否是组件
  _propKeys?: Array<string>; // props传入对象的键数组
  _parentVnode?: VNode; // 当前组件，在父组件中的VNode对象
  _parentListeners?: ?Object; // 当前组件，在父组件上绑定的事件
  _renderChildren?: ?Array<VNode>; // 父组件中定义在当前元素内的子元素的VNode数组（slot）
  _componentTag: ?string;  // 自定义标签名
  _scopeId: ?string;
  _base: Class<Component>; // Vue
  _parentElm: ?Node; // 当前自定义组件的父级dom结点
  _refElm: ?Node; // 当前元素的nextSlibing元素，即当前dom要插入到_parentElm结点下的_refElm前
}
```

更多内容请参考[Vue文档之API](https://cn.vuejs.org/v2/api/)



### Vue的生命周期和钩子函数

每一个Vue实例在创建时都需要经过一系列的初始化过程，例如：设置数据监听、模板编译、将实例挂载到DOM并在数据变化时更新DOM等。同时也会运行一些叫做**生命周期钩子**的函数。

如果有些朋友学过Java的话，那么对于Servlet的生命周期应该不陌生吧！(扯远了)，没有学过的朋友也没有关系，毕竟我们主要讲的Vue的生命周期和在它生命周期里的一些钩子函数。
![](https://s1.ax1x.com/2020/06/02/tNHzfU.jpg)

为了更好的讲解Vue的生命周期。我从官网偷了一张图献给大家。

![](https://s1.ax1x.com/2020/06/06/t6P5tA.png)

这张图对于Vue的生命周期和钩子函数说的非常的明白。下面我们看一张关于Vue生命周期中出现的钩子函数示意图。

![](https://img2018.cnblogs.com/i-beta/1475945/201912/1475945-20191229112739585-1787919479.png)



在这里我主要讲解常用的八个生命周期的钩子函数。其它的了解一下就可以了



##### beforeCreate(实例创建前)

- 实例组件刚开始创建，元素dom和数据都还没有初始化

- 应用场景：可以在这加个loading事件



##### created(实例创建后)

- 数据data已经初始化完成，方法也已经可以调用，但是dom为渲染，在这个周期里面如果进行请求是可以改变数据并渲染，由于dom未挂载，请求过多或者占用时间过长会导致页面线上空白
- 应用场景：在这结束loading，还做一些初始化，实现函数自执行 



##### beforeMoute(元素挂载前)

- dom未完成挂载，数据初始化完成，但是数据的双向绑定还是{{}}，这是因为vue采用了虚拟dom技术



##### mouted(元素挂载后)

- 数据和dom都完成挂载，在上一个周期占位的数据把值渲染进去，一般请求会放在这个地方，因为这边请求改变数据之后刚好能渲染



##### beforeUpdate(实例更新前)

- 只要是页面数据改变了都会触发，数据更新之前，页面数据还是原来的数据，当你请求赋值一个数据的时候就会执行这个周期，如果没有数据改变不执行



##### updated(实例更新后)

- 只要是页面数据改变了都会触发，数据更新完毕，页面的数据是更新完成的



> beforeUpdated和updated要谨慎使用，因为页面更新数据的时候都会触发，在这里操作数据很影响性能和死循环



##### beforeDestory(实例销毁前)

- 实例销毁之前调用，在这一步，实例仍然完全可用



##### destory(实例销毁后)

- Vue实例销毁后调用，调用后，Vue实例指示的所有内容都会解除绑定，所有的事件监听器都会被移除，所有的子实例也会被销毁



讲一下开发者经常会犯的错误，就是关于Vue的钩子函数中使用箭头函数的问题。这个问题觉得有必要提出来，毕竟自己在开发过程中，经常会踩这些坑。



> 生命周期钩子的 `this` 上下文指向调用它的 Vue 实例



不要在选项 property 或回调上使用箭头函数，比如 

> created()=>console.log('a')或者vm.$watch('a',newValue=>this.myMethod())，因为箭头函数并没有this，this会作为变量一直向上级词法作用域查找，直至找到为止。



经常出现如下错误

- Uncaught TypeError: Cannot read property of undefined
- Uncaught TypeError: this.myMethod is not a function

这一点需要非常注意。



#### 控制台输出福利

console.log支持的格式标志有:

![](https://img2018.cnblogs.com/blog/63651/201812/63651-20181219183452516-2088034769.png)

**示例：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<script>
   const tom={name:"杨戬", age:18}
    console.group("开始");
    console.group("第一组");
    console.log("%c%s%o","background:red;color:yellow;",'对象是：',tom);
    console.groupEnd();

    console.group("第二组");
    console.log("%c%s%o","background:red;color:yellow;",'对象是：',tom);
    console.groupEnd();

    console.group("第三组");
    console.log("%c%s%o","background:red;color:yellow;","对象是:",tom)
</script>
</body>
</html>
```

结果：

![](https://s1.ax1x.com/2020/06/06/t6Z4Dx.png)



接下来通过两个示例对Vue的生命周期进行解析

#### Vue生命周期示例一

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <input type="text" v-model="msg">
    {{msg}}

</div>
<button onclick="destroy()">销毁</button>
<script src="../js/vue.js"></script>
<script>
    const vm=new Vue({
        el:'#app',
        data:{
            msg:"Vue"
        },
        beforeCreate:function () {
            console.log("Vue实例创建前："+this.msg,this.$el);
            //  数据data和dom都没有初始化
        },
        created:function () {
            console.log("Vue实例创建后:"+this.msg,this.$el);
            //  数据data初始化完成，dom还没有初始化完成

        },
        beforeMount:function () {
            console.log("Vue实例挂载前"+this.msg,this.$el);

        },
        mounted:function () {
            console.log("Vue实例挂载后:"+this.msg,this.$el);

        },
        beforeUpdate:function () {
            console.log("Vue实例更新前:"+this.msg,this.$el);
        },
        updated:function () {
            console.log("Vue实例更新后:"+this.msg,this.$el);
        },
        beforeDestroy:function () {
            console.log("Vue实例销毁前:"+this.msg,this.$el);
        },
        destroyed:function () {
            console.log("Vue实例销毁后:"+this.msg,this.$el);
        }

    })
    function destroy() {
        vm.$destroy();
    }
</script>
</body>
</html>

```



![](https://s1.ax1x.com/2020/06/06/t6lI4P.png)



#### Vue生命周期示例二

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    {{name}}
</div>
<button onclick="destroy()">销毁</button>
<script src="../js/vue.js"></script>
<script>
    const vm=new Vue({
        el:'#app',
        data:{
            name:"杨戬",
            age:18
        },
        beforeCreate:function () {
            console.group("Vue实例创建前");
            console.log("数据是:"+this.$data);
            console.log("挂载的元素是:"+this.$el);
            console.groupEnd();
        },
        created:function () {
            console.group("Vue实例创建后");
            console.log("数据是:"+JSON.stringify(this.$data));
            console.log("挂载的元素是:"+this.$el);
            console.groupEnd();

        },
        beforeMount:function () {
            console.group("Vue实例挂载前");
            console.log("数据是:"+JSON.stringify(this.$data));
            console.log(this.$el);
            console.groupEnd();

        },
        mounted:function () {
            console.group("Vue实例挂载后");
            console.log("数据是:"+JSON.stringify(this.$data));
            console.log(this.$el);
            console.groupEnd();

        },
        beforeUpdate:function () {
            console.group("Vue实例更新前");
            console.log("数据是:"+JSON.stringify(this.$data));
            console.log(this.$el);
            console.groupEnd();
        },
        updated:function () {
            console.group("Vue实例更新后");
            console.log("数据是:"+JSON.stringify(this.$data));
            console.log(this.$el);
            console.groupEnd();
        },
        beforeDestroy:function () {
            console.group("Vue实例销毁前");
            console.log("数据是:"+JSON.stringify(this.$data));
            console.log(this.$el);
            console.groupEnd();
        },
        destroyed:function () {
            console.group("Vue实例销毁后");
            console.log("数据是:"+JSON.stringify(this.$data));
            console.log(this.$el);
            console.groupEnd();
        }
    });
    function destroy() {
        vm.$destroy();
    }
</script>
</body>
</html>

```



![](https://s1.ax1x.com/2020/06/06/t6Y5Nj.png)

通过两个实例的学习，对Vue的生命周期有一定的了解，可能有些朋友没有领悟到其精髓，但是随着深入学习，我想大家会慢慢领悟到的。

![](https://s1.ax1x.com/2020/06/06/t6t3qS.jpg)



接下来总结一下：

- beforeCreate()：此时$el、data 的值都为undefined，即el 和 data 并未初始化 
- created()：此时可以拿到data的值，但是$el依旧为undefined，即data完成了数据的初始化，el没有
- beforeMount()：$el的值为“虚拟”的元素节点，dom未完成挂载，数据初始化完成，但是数据的双向绑定还是{{}},这是因为vue采用了虚拟dom技术
- mounted()： 数据和dom都完成挂载，在上一个周期占位的数据把值渲染进去，一般请求会放在这个地方，因为这边请求改变数据之后刚好能渲染

![](https://img2018.cnblogs.com/i-beta/1475945/201912/1475945-20191229114711306-54699219.png)



### Vue实例的手动挂载和调用事件

vm.＄mount( [elementOrSelector] ) 如果 Vue 实例在实例化时没有收到 el 选项，则它处于“未挂载”状态，没有关联的 DOM 元素。可以使用 vm.＄mount() 手动地挂载一个未挂载的实例，学习手动挂载和调用事件之前，我提取了一些vue实例常用的属性和方法，带有前缀 ＄ 便于与代理的data区分

- vm.＄el：类型（HTMLElement）挂载元素，Vue实例的DOM根元素。即vm.$el===document.getElementById('节点')，注意：相等的情况必须是实例创建之后才行，也就是created之后

- vm.＄data：类型（Object），Vue实例观察的数据对象

- vm.＄props：类型（Object），当前组件接收到的 props 对象。Vue 实例代理了对其 props 对象属性的访问。

- vm.＄options：类型（Object），用于当前 Vue 实例的初始化选项。需要在选项中包含自定义属性时会有用处

- vm.＄parent：类型（Vue实例），父实例，如果当前实例有的话

- vm.＄root：类型（Vue实例），当前组件树的根 Vue 实例。如果当前实例没有父实例，此实例将会是其自己。

- vm.＄children：类型（Array(Vue实例)），当前实例的直接子组件。需要注意 `$children` 并不保证顺序，也不是响应式的。如果你发现自己正在尝试使用 `$children` 来进行数据绑定，考虑使用一个数组配合 `v-for` 来生成子组件，并且使用 Array 作为真正的来源。

#### 手动挂载

接下来是介绍手动挂载和调用事件的常用方法，共有三个

```javascript
var MyComponent = Vue.extend({
template: '<div>Hello!</div>'
})

// 创建并挂载到 #app (会替换 #app)
new MyComponent().＄mount('#app')

// 同上
new MyComponent({ el: '#app' })

// 或者，在文档之外渲染并且随后挂载
var component = new MyComponent().＄mount()
document.getElementById('app').appendChild(component.＄el)
```



实例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app"></div>
<button onclick="handleMount1()">手动挂载方式一</button>
<button onclick="handleMount2()">手动挂载方式二</button>
<button onclick="handleMount3()">手动挂载方式三</button>
<script src="../js/vue.js"></script>
<script>
    const vm=new Vue({
        data:{
            name:'杨戬'
        },
        template: "<h2>{{name}}</h2>"
    });
    //  调用手动挂载方式一
    function handleMount1() {
        //  手动挂载到指定DOM元素
        vm.$mount("#app")
    }
    //  调用手动挂载方式二
    function handleMount2() {
        //  手动挂载，触发编译
        vm.$mount();
        //将编译要生成的内容元素添加到要挂在的DOM元素中，作为子元素
        document.getElementById("app").appendChild(vm.$el);

    }
    //  调用手动挂载方式三
    function handleMount3() {
        //  扩展出一个新的Vue构造器
        const Component=Vue.extend({
            template:"<h2>{{name}}</h2>"
        });
        const vm01=new Component({
            el:'#app',
            data:{
                name:"杨戬"
            }
        })

    }
</script>
</body>
</html>

```

大家可以尝试点击按钮试试，看下实例是否挂载成功。



#### 销毁实例

vm.＄destroy() 完全销毁一个实例。清理它与其它实例的连接，解绑它的全部指令及事件监听器，

这是实例的时候有写的到这个方法，大家可以回过头去看。



#### 强制更新

vm.＄forceUpdate() 迫使 Vue 实例重新渲染。注意它仅仅影响实例本身和插入插槽内容的子组件，而不是所有子组件。



### 结尾

如果觉得本篇文章对您有用的话，可以麻烦您给笔者点亮那个点赞按钮。
<img src="https://s1.ax1x.com/2020/03/23/8oGjfA.th.jpg">

对于杨戬这个暖男来说：**真的真的非常有用**，您的支持将是我继续写文章前进的动力，我们下篇文章见。

**【原创】|二郎神杨戬**

> 原创不易，莫要白嫖。
> 二郎神杨戬，一个在互联网前端苟且偷生的划水程序员，专注于前端开发，善于技术分享。
> 如需转载，请联系作者或者保留原文链接，微信公众号搜索二郎神杨戬或者扫描下方的二维码更加方便。
>
> 一起来见证二郎神杨戬的成长吧！更多好文、技术分享尽在下方这个公众号。欢迎关注。

<img src="https://s1.ax1x.com/2020/05/04/Y9LspR.png" />