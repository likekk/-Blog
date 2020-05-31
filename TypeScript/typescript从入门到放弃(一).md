>  先点赞后关注，防止会迷路

> 寄语：长风破浪会有时，直挂云帆济沧海。
> 本文已收录至[https://github.com/likekk/-Blog](https://github.com/likekk/-Blog)欢迎大家star :smile::smile::smile: ,共同学习，共同进步。如果文章有错误的地方，欢迎大家指出。后期将在将github上规划前端学习的路线和资源分享。

### 前言
亲爱的读者们，大家好，我是杨戬，一个在互联网前端苟且偷生的划水程序员，本编文章开始将带你入坑TypeScript。

个人认为TypeScript的前景还是可以的（可以接受反驳），怎么说呢？现在很多的框架已经从JavaScript向TypeScript拥抱了，谷歌也在大力支持TypScript的扩展，谷歌的Angular2.x+就是基于TypeScript，而且Vue3.0也在使用TypeScript进行重构（道听途说），我也不逼逼那么多了，我们直接开始吧！

[![tMq641.jpg](https://s1.ax1x.com/2020/05/30/tMq641.jpg)](https://imgchr.com/i/tMq641)



###  TypeScript介绍

介绍的话我就直接引用一些吧！毕竟有些东西肯定比我讲的好（拥有一颗谦卑的心），

- TypeScript 是 JavaScript 的一个超集，支持 ECMAScript 6 标准，TypeScript扩展了JavaScript的语法。

- TypeScript 由**微软**开发的自由和开源的编程语言。

- TypeScript 设计目标是开发大型应用，它可以编译成纯 JavaScript，编译出来的 JavaScript 可以运行在任何浏览器上
- 谷歌也在大力支持TypScript的扩展，谷歌的angular2.x+就是基于TypeScript
- 最新的Vue、React也可以集成TypeScript
- Node.js的框架nest.js、midway中用的就是TypeScript的语法

这里我多说一句：TypeScript入门十分简单，只要你有JavaScript语言的基础，那么学习TypeScript起来成本是相对较低的，可以不用像学习一门新的语言那样费劲。



### TypeScript语言特性

TypeScript 是一种给 JavaScript 添加特性的语言扩展。在其上扩展的功能有许多，我们一起来看下都扩展了哪些功能。

- 类型批注和编译时类型检查
- 类型推断和类型擦除
- 接口（interface）、枚举（enum）、Mixin
- 泛型编程<T>（很多编程语言都有）
- 名字空间（namespace）
- 元组（tuple）
- Await

当然还有一些功能是从ES6移植过来的

- 类（Class）
- 模块（module）
- lambda函数的箭头语法
- 可选参数和默认参数

简单说几点JavaScript和TypeScript的区别

- TypeScript是JavaScript的超集，扩展了JavaScript的语法，因此现有的JavaScript代码可与TypeScript**一起工作无需任何修改**，TypeScript通过类型注解提供编译时的静态类型检查。
- TypeScript可处理已有的JavaScript代码，并只对其中的TypeScript代码进行编译

### TypeScript的优点VSTypescript的缺点

#### TypeScript的优点

- TypeScript增加了代码的可读性和可维护性
- TypeScript非常包容
- TypeScript拥用活跃的社区



#### TypeScript的缺点

- 有一定的学习成本，需要理解接口（Interfaces）、泛型（Generics）、类（Classes）、枚举类型（Enums）等前端工程师可能不是很熟悉的概念
- 短期可能会增加一些开发成本，毕竟要多写一些类型的定义，不过对于一个需要长期维护的项目，TypeScript 能够减少其维护成本
- 集成到构建流程需要一些工作量
- 可能和一些库结合的不是很完美



### TypeScript安装，编译

首先需要安装TypeScript，必须有Node.js的环境，关于Node.js的安装环境推荐大家这一篇博文

[Node.js安装配置教程](https://www.cnblogs.com/zhouyu2017/p/6485265.html)，写得非常详细。

安装完成之后，我们使用命令行看下是否安装成功。



> node -v 检查node版本



[![tMxU3R.png](https://s1.ax1x.com/2020/05/30/tMxU3R.png)](https://imgchr.com/i/tMxU3R)

node.js环境配置成功之后，我们全局安装一下TypeScript，这里有几种方法供大家使用，大家选择自己喜欢的方法就可以了。

- 使用npm命令全局安装

> npm install -g typescript



- 使用cnpm命令安装

> npm install cnpm --registry=https://registry.npm.taobao.org
>
> cnpm install -g typescript



- 使用yarn命令安装

> npm install -g yarn 或者 cnpm install -g yarn  
>
> yarn global add typescript



安装完成之后，我们检查TypeScript是否安装成功

> 检查命令 tsc -v



如果出现版本信息，那么一般都是安装成功了，这里就不进行截图了

开发工具推荐使用 vscode进行开发，vscode也是微软旗下的产品，使用vscode开发TypeScript，只能用下面那张图来表达我内心的感受。

[![tQS4AS.jpg](https://s1.ax1x.com/2020/05/30/tQS4AS.jpg)](https://imgchr.com/i/tQS4AS)

当然也还有许多优秀的开发工具，但是我还是首选vscode。

[![tllr7T.jpg](https://s1.ax1x.com/2020/05/31/tllr7T.jpg)](https://imgchr.com/i/tllr7T)



### TypeScript的HelloWorld

所有的一切准备好之后，那就开始我们的开发之旅吧！

首先我们新建一个文件夹，创建好文件夹之后我们新建一个.ts为后缀名的文件，目录结构如下

[![tQ9tZ6.png](https://s1.ax1x.com/2020/05/30/tQ9tZ6.png)](https://imgchr.com/i/tQ9tZ6)

然后我们在index.ts文件内编写helloworld代码



```typescript
let str:string="Hello World"
console.log(str)
```



TypeScript 转换为 JavaScript 过程如下图：

[![tl8Xv9.png](https://s1.ax1x.com/2020/05/31/tl8Xv9.png)](https://imgchr.com/i/tl8Xv9)

刚开始看到这段代码的时候瞬间有JavaScript的影子，和JavaScript声明的变量的代码差不多，就是指定了类型。比较严谨。



由于浏览器是无法识别TypeScript的，所以我们需要将TypeScript进行编译成JavaScript语言，让浏览器可以识别。



> tsc index.ts（直接在vscode的控制台执行）



编译之后的代码（index.js）：

```javascript
var str = "Hello World";
console.log(str);
```



此时编译成功之后该文件夹会自动生成index.js文件，而这个文件就是index.ts进行编译之后的文件。然后我们在新建index.html文件，引入编译之后的inde.js文件。文件目录如下。

[![tl1iCQ.png](https://s1.ax1x.com/2020/05/31/tl1iCQ.png)](https://imgchr.com/i/tl1iCQ)

之后运行index.html文件就可以看到输出结果了。



### TypeScript开发工具vscode自动编译.ts文件

我们想一个这样的问题，如果每次写一段代码都需要自己编译一下，试想一下工作量有多么大，那么有没有可能可以实现一边写代码一边让它自己进行编译呢？答案是肯定的。

##### 1、使用vscode的控制台输入tsc --init命令



- 选择typescript选项
- tsc:watch -tsconfig.json

完成这几个步骤之后你就可以疯狂编码了。

[![tl8a1H.jpg](https://s1.ax1x.com/2020/05/31/tl8a1H.jpg)](https://imgchr.com/i/tl8a1H)



### 结尾

如果觉得本篇文章对您有用的话，可以麻烦您给笔者点亮那个点赞按钮。
![](https://s1.ax1x.com/2020/03/23/8oGjfA.th.jpg)

对于杨戬这个暖男来说：**真的非常有用**，您的支持就是我前进的动力，我们下篇文章见。

**【原创】|杨戬**

> 原创不易，请勿白嫖。
> 二郎神杨戬，一个在互联网前端苟且偷生的划水程序员，专注于前端开发，善于技术分享。
> 如需转载，请联系作者或者保留原文链接，微信公众号搜索二郎神杨戬。

<img src="https://s1.ax1x.com/2020/05/04/Y9LspR.png" />