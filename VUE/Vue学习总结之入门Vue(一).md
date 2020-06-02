> 点赞再看、养成习惯。
>
> 寄语：长风破浪会有时，直挂云帆济沧海。
> 本文已收录至[https://github.com/likekk/-Blog](https://github.com/likekk/-Blog)欢迎大家star :smile::smile: :smile: ,共同学习，共同进步。如果文章有错误的地方，欢迎大家指出。后期将在将github上规划前端学习的路线和资源分享。

### 前言

大家好，我是杨戬，一个在互联网前端苟且偷生的划水程序员，从本篇博文开始，我将会撰写一系列关于vue.js的优质文章，坚持输出，一方面好久没有使用过vue.js框架了，之前在博客园陆陆续续的写过一些文章，但是自我感觉不太合格，在一个夜黑风高的夜晚决定痛定思痛重新撰写这个系列。希望大家可以多多支持我喔!

文章部分内容可能有误，如果读者有更好的解答方案，可以在下方留下您的评论，我将在第一时间进行更改错误内容，在此，非常感谢各位读者。



### 正文

#### 认识vue.js

既然是学习vue.js我们就必须知道vue.js到底是什么，在这里杨戬就不过多的解释了，我们看下官方文档的解释。



>Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。



官方的解释已经非常的清晰明了，在这里杨戬也为我最爱的读者们献上一张关于vue的图。



![](https://s1.ax1x.com/2020/06/03/tNxHZ4.png)



#### 声明式渲染

可以简单的理解vue中一些常见的指令，例如：v-if、vue-for、vue-html等等。



#### 组件系统

组件系统是vue.js里面非常强大的一个功能、涉及比较复杂，在这里不过多进行描述、后期的话会一步一步的细讲。常用的有父子组件通信、组件的一些校验等等。



#### 客户端路由

客户端路由的话可以理解为一个链接，通常就是我们在html里面的a标签（个人认为，接受反驳）。根据不同的路径跳转到不同的界面(组件)，通常在做SPA单页应用的时候经常用到。



#### 状态管理

状态管理主要是用于开发大型应用，对一些公共的数据进行管理，因为某些数据可能在多个组件中使用到，对于父子组件来说是比较容易。

但是对于非父子组件来说，如果某些数据在很多地方使用到，那么对于数据的管理就会非常混乱。所以状态管理（vuex）是将这些数据进行统一的管理起来（个人的理解，接受反驳）。



#### 构建工具

构建工具主要是vue-cli、webpack等等。



### 框架和库的区别

一提到框架，很多人就会联想到库，毕竟在没有接触到框架之前我们都是使用库的(jQuery、zepto)，那么什么是库，什么是框架呢？我总结如下：

#### 框架

框架是为了解决一类问题而开发出来的产品，基于自身的特点向用户提供一套完整的解决方案。常见的前端框架有：



> Vue、React、Angular|Angular2



在这里如果不太了解框架的意思，你可以这样理解，框架的话，主动权在它手上，我们必须遵守它制定的一系列规则，如果我们不遵守的话，我们就使用不了框架或者框架会抛出异常信息。



> 例如：在vue中数据必须写在data中，方法必须写在methods中，当然有些既可以当做方法也可以当做计算属性。这个我们后面会提到，现在只是抛砖引玉。



#### 库

库是将代码集合成一个产品，供开发者去使用，开发者去调用库中的方法去实现自己的功能，例如：jQuey、zepto。



库的话我们就是拿来即用，之前也没有去想过或者弄懂库是什么东西，我自己总结是：库的主动权在我们手上。



例如：在jQuery中我们获取某个节点是$('[类名/id]')这种操作，但是我们也可以使用JavaScript中的原生方法document.getElementById('id')或者document.getElementsByClassName('class')。



主动权在我们自己的手上，我们想使用jQuey中的方法就使用jQuery中的方法，想使用原生的JavaScript方法就使用JavaScript原生的方法，自己可以为所欲为。

#### vue.js的优点

- 易用：会html、css、js即可上手

- 灵活：不断繁荣的生态系统，可以在一个库和一套完整框架之间自如伸缩

- 高效：20kB min+gzip大小，超快虚拟DOM,最省心的优化



接下来我们如何引用vue.js

### 起步

这里提供引入vue.js的3种方法、各位读者根据需要按照自己喜欢的方式引入即可。

1、直接script标签引入

直接下载并用 `<script>` 标签引入，`Vue` 会被注册为一个全局变量。

下载地址：[vue.js地址](https://github.com/vuejs/vue )

2、CDN方式引入

对于制作原型或学习，你可以这样使用最新版本

```
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```



对于生产环境，推荐链接到一个明确的版本号和构建文件，以避免新版本造成的不可预期的破坏：

```javascript
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>
```



如果你使用原生 ES Modules，这里也有一个兼容 ES Module 的构建文件：

```
<script type="module">
  import Vue from 'https://cdn.jsdelivr.net/npm/vue@2.6.11/dist/vue.esm.browser.js'
</script>
```



3、NPM的方式引入

```javascript
npm install vue
```



引入成功之后、我将带领读者们一起走进vue.js的开发世界。

![](https://s1.ax1x.com/2020/06/02/tNHzfU.jpg)



#### 声明式渲染

Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<div id="app">
    <span>{{message}}</span>
</div>
<script src="js/vue.js"></script>
<script>
    const vm=new Vue({
        el:"#app",  //  挂载DOM的根元素
        data:{
            message:"Hello world"
        }
    })
</script>
</body>
</html>
```

这里需要注意一下：

- el表示vue.js挂载DOM的根元素，如果其它元素想要使用vue.js的语法，那么必须要在挂载了vue.js实例里面

- 此时message是响应式的数据，如何证明，下篇文章为你揭开它的真面目。



除了文本插值，我们还可以像这样来绑定元素 attribute：

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <span v-bind:title="message">鼠标悬停几秒钟查看此处动态绑定的提示信息！</span>
</div>
<script src="../js/vue.js"></script>
<script>
    const vm=new Vue({
        el:'#app',
        data:{
            message: '页面加载于 ' + new Date().toLocaleString()
        }
    })
</script>
</body>
</html>
```

`v-bind` attribute 被称为**指令**，指令带有前缀 `v-`，以表示它们是 Vue 提供的特殊 attribute 

v-bind:用来绑定属性的。



> v-bind:src、v-bind:title、:src、:title



当然v-bind也可以直接改写成**：**，去掉前面的v-bind



#### 条件与循环

1、条件if示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<div id="app">
    <span v-if="show">你可以看到我</span>
    <span v-if="bl">你看不到我</span>
</div>
<script src="../js/vue.js"></script>
<script>
    const vm=new Vue({
        el:'#app',
        data:{
            show:true,
            bl:false
        }
    })
</script>
</body>
</html>
```



2、循环for示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<div id="app">
    <ul v-for="(item,index) of todos">
        <li>{{item.text}}</li>
    </ul>
</div>
<script src="../js/vue.js"></script>
<script>
    const vm=new Vue({
        el:'#app',
        data:{
            todos:[
                {text:"学习JavaScript"},
                {text:"学习Vue"},
                {text:"学习React"}
            ]
        }
    })
</script>
</body>
</html>
```



#### 处理用户输入、表单

1、用 `v-on` 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <p>{{message}}</p>
    <button v-on:click="reverseMessage">反转消息</button>
</div>
<script src="../js/vue.js"></script>
<script>
    const vm=new Vue({
        el:'#app',
        data:{
            message: 'Hello Vue.js!'
        },
        methods:{
            reverseMessage:function () {
                this.message=this.message.split('').reverse().join('');
            }
        }
    })
</script>
</body>
</html>
```



2、表单输入

Vue 还提供了 `v-model` 指令，它能轻松实现表单输入和应用状态之间的双向绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<div id="app">
    <p>{{message}}</p>
    <input type="text" v-model="message">
</div>
<script src="../js/vue.js"></script>
<script>
    const vm=new Vue({
        el:'#app',
        data:{
            message:"你好"
        }
    })
</script>
</body>
</html>

```





#### 组件应用构建

组件系统是 Vue 的另一个重要概念，因为它是一种抽象，允许我们使用小型、独立和通常可复用的组件构建大型应用。仔细想想，几乎任意类型的应用界面都可以抽象为一个组件树：

![](https://s1.ax1x.com/2020/06/03/tNvKc8.png)

在 Vue 里，一个组件本质上是一个拥有预定义选项的一个 Vue 实例。在 Vue 中注册组件很简单：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <ul>
        <todo-item></todo-item>
    </ul>
</div>
<script src="../js/vue.js"></script>
<script>
    Vue.component('todo-item', {
        template: '<li>这是个待办项</li>'
    })
    const vm=new Vue({
        el:'#app',
        data:{

        }
    });
</script>
</body>
</html>

```



但是这样会为每个待办项渲染同样的文本，这看起来并不炫酷。我们应该能从父作用域将数据传到子组件才对。让我们来修改一下组件的定义，使之能够接受一个 prop

```javascript
Vue.component('todo-item', {
  // todo-item 组件现在接受一个
  // "prop"，类似于一个自定义 attribute。
  // 这个 prop 名为 todo。
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```



现在，我们可以使用 `v-bind` 指令将待办项传到循环输出的每个组件中：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <ul>
        <todo-item
                v-for="item in groceryList"
                v-bind:todo="item.text"
                v-bind:key="item.id"
        ></todo-item>
    </ul>
    <ul>
        <todo-item
            v-for="(item,index) of productList"
            v-bind:todo="item.name"
            v-bind:key="item.id"
        ></todo-item>
    </ul>
</div>
<script src="../js/vue.js"></script>
<script>
    Vue.component('todo-item', {
        props:["todo"],
        template: '<li>{{todo}}</li>'
    })
    const vm=new Vue({
        el:'#app',
        data:{
            groceryList: [
                { id: 0, text: '蔬菜' },
                { id: 1, text: '奶酪' },
                { id: 2, text: '随便其它什么人吃的东西' }
            ],
            productList:[
                {id:1001,name:"苹果"},
                {id:1002,name:"香蕉"},
                {id:1003,name:"菠萝"},
                {id:1004,name:"水蜜桃"}
            ]
        }
    });
</script>
</body>
</html>

```



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

<img src="https://s1.ax1x.com/2020/05/04/Y9LspR.png" style="margin:0 auto" />