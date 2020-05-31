> 先点赞后关注，防止会迷路

> 寄语：长风破浪会有时，直挂云帆济沧海。
> 本文已收录至[https://github.com/likekk/-Blog](https://github.com/likekk/-Blog)欢迎大家star :smile::smile: :smile: ,共同学习，共同进步。如果文章有错误的地方，欢迎大家指出。后期将在将github上规划前端学习的路线和资源分享。

![本章思维导图](https://s1.ax1x.com/2020/05/04/Y9qMGR.png)

### 前言

这是ES6的第二篇文章，主要讲解变量解构赋值的类型和用途，大家可以根据思维导图大概的了解一下本文需要学习的知识和重点内容。



### 数组的解构赋值

数组的解构赋值是这篇博客需要讲解的第一个知识点，数组的解构赋值就像是玩开心消消乐一样，开心消消乐这个游戏的规则（**我大概知道一点点，别喷我!**）匹配邻近相同的色块消失，然后加分。

而对于数组解构，匹配到相同的模式，我们取到相对应的值，没有匹配到的话，值为undefined。

那么就让我们一起用玩开心消消乐的方式学习数组的解构赋值。



##### 1、基本用法

讲解每一个知识点的开始首先都是需要先讲解它的基本概念(**数据的解构赋值比较简单，暂时没有什么概念**)，然后是讲解它的用法，我就直接跳过第一个直接进入第二个了。先来看下简单的示例。

我们以前定义变量的形式是这样的

```js
let a;
let b;
let c;
```

还有这样的

```javascript
let a,
    b,
    c;
```

这些看起来在一定的美观上还是稍微逊色了一点，升级一下得到如下的风格。

```javascript
let [a,b,c]=[1,2,3];
console.log(a);	//	1
console.log(b);	//	2
console.log(c);//	3
```

有木有觉得瞬间上升了一个档次，很beautiful。

开始的时候的也说了，匹配成功，取得相对应的值，匹配不成功值为undefined，现在排上用场了。

```
let [bar]=[];
console.log(bar);	//	undefined

let [a,b]=[1];
console.log(a);		//	1
console.log(b);		//	undefined
```

可以看到在第二个示例中，a解构成功，但是b没有解构成功，所以b的取值为undefined。

##### 2、不完全解构

> 所谓的不完全解构就是模式并没有完全匹配



```javascript
let [x,y]=[1,2,3];
console.log(x); //  1
console.log(y);//   2

let [a,[b],d]=[1,[2,3],4];
console.log(a); //  1
console.log(b); //  2
console.log(d);//   4
```

这两个示例中，都是不完全解构。



##### 3、默认值

数组的解构赋值允许我们使用一些默认值。但是有个前提条件是：

> 当一个数组成员严格等于(===)undefined时，默认值才会生效



```javascript
let [foo=true]=['1'];	//true
let [a='1']=[undefined];//1;
let [a='2']=[null];	//	null
```

> 注意：undefined!==null



##### 4、特殊值

像有些特殊值，它是会解构失败的，（No，No，No）准确的说："不可遍历的解构(不具备Iterator接口)会解构失败"，

```javascript
let [a]=1;
let [b]=false;
let [c]=NaN;
let [d]=undefined;
let [e]=null;
let [f]={};
```

以上这些特殊值，都会解构失败，大家注意一下就可以了。



### 对象的解构赋值

解构赋值不仅可以用于数组，还可以用于对象等其它类型，对象的解构赋值也十分简单，个人觉得主要是键的匹配成功就可以。即：**变量和属性同名就可以**。



##### 1、基本用法

```javascript
let {foo,bar}={foo:1,bar:2}
console.log(foo);	//	1
console.log(bar);	//	2
```



**注意：**

> 前面的foo、bar这两个属性都是值，而不是键，因为在ES6中，如果对象的属性名和属性值相同的话键可以不用写（没有记错的话）。



```javascript
let {foo:baz,bar:bar,baa}={foo:1,bar:2}
console.log(baz);	//	1
console.log(bar);	//	2
console.log(baa);	//	undefined
```

这个示例的话就很容易看出，然后解构失败的话，值同样为undefined。



###### 1.1升级玩法一



上面的这些对象的解构赋值都是没有嵌套的，我们来试下嵌套的解构赋值能否成功

```javascript
let obj={
    p:[
        'hello',
        {y:"world"}
    ]
}
let {p:[a,{y}]}=obj;
console.log(a);	//	hello
console.log(y);	//	world
```



> 由于hello这个属性值的键我们没有特殊指定，所以在这里使用任意一个变量接收都是可以的，但是world属性值的键我们指定了，所以必须使用y这个变量接收，否则会出现undefined。还有一点就是解构赋值的时候模式一定要相同。



###### 1.2升级玩法二



我们看下另外一个示例：

```javascript
const code={
    foo:{
        start:{
            a:1,
            b:2,
        }
    }
}
const {foo,foo:{start},foo:{start:{a}},foo:{start:{b}}}=code;
console.log(foo);
console.log(start);
console.log(a);
console.log(b);
```

我们主要为foo、start、a|b进行了解构，当解构a、b时，foo和start均为模式匹配。只有a、b是变量。



对象解构赋值有一点比较强大的是，解构赋值可以取到继承的属性

```javascript
const child={};
const parent={foo:'bar'};
Object.setPrototypeOf(child,parent);
const {foo}=child;
console.log(foo);	//	bar
```

child这个对象原来什么属性都没有，但是通过继承，获得了parent对象foo的属性值。个人认为这一点是比较强大的。



##### 2、默认值

同样，对象解构也有默认值

```javascript
let {a=3}={};
console.log(a); //  3
let {x,y=3}={x:1}
console.log(x); //  1
console.log(y); //  3
let {x:y=3}={};
console.log(y); // 3
let {x:y=3}={x:5};
console.log(y); //  5
let {msg:msg="hello"}={};
console.log(msg);   //hello
```

默认值的条件和之前的一样也是：



>  **对象的属性值严格不等于undefined**



```javascript
let {x:3}={x:undefined};
let {y:3}={y:null};
console.log(x);	//	3
console.log(y);	//	null
```



### 字符串的解构赋值



> 字符串被转换成了一个类似数组的对象



```javascript
const [a,b,c,d]="good";
console.log(a);//g
console.log(b);//o
console.log(c);//o
console.log(d);//d
```



这里说明一下，类似数组的对象都有一个**length**属性，因此还可以对这个属性解构赋值



```javascript
const {length:len}="good";
console.log(len);
```



### 数值和布尔值的解构赋值



**温馨提示：**

> 解构赋值时，如果等号右边是数值和布尔值，则会先转换为对象，（调用toString方法）



```javascript
let {toString:a}=123;
console.log(a===Number.prototype.toString);
let {toString:b}=true;
console.log(b===Boolean.prototype.toString);
```



**温馨提示：**

>解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。由于`undefined`和`null`无法转为对象，所以对它们进行解构赋值，都会报错。



```javascript
let {a:b}=undefined;
let {x:y}=null;
```



### 函数参数的解构赋值



##### 1、基本用法

```javascript
function bar([x,y]) {
    return x+y;
}
console.log(bar([1,2]));//3

[[1,2],[3,4]].map(([a,b])=>{
    console.log(a+b);//3,7
})
```



##### 2、使用默认值

 函数参数的解构赋值同样也有默认值，我们来看下特别有意思的示例

```
function foo({x=0,y=0}={}) {
    return [x,y]
}
console.log(foo({x:1,y:2}));//1,2
console.log(foo({x:1}));//1,0
console.log(foo({y:2}));//0,2
console.log(foo({}));//0,0
console.log(foo());//0,0

function bar({x,y}={x:0,y:0}) {
    return [x,y];
}
console.log(bar({x:1,y:2}));//1,2
console.log(bar({x:1}));//1,undefined
console.log(bar({y:2}));//undefined,2
console.log(bar({}));//undefined,undefined
console.log(bar());//0,0
```

在函数foo中，我们为变量x，y指定默认值，但是在函数bar中我们是为函数参数指定默认值而不是变量x，y指定。所以得到的结果不一样，undefined会触发函数参数的默认值。



### 解构赋值的用途

讲了那么多的解构赋值的类型，肯定也需要知道它们的用途吧！通过思维导图我们应该很清楚的知道了我所需要讲解的内容。接下来就对解构赋值的用途进行一一讲解。



##### 1、交换变量的值

对于交换变量的值的应用，有一个非常经典的题目，我们一起来看下。题目大概和网上的差不多，具体的记不太清楚了，意思就是：

> 定义a,b两个变量。不定义第三个变量的情况下，交换两个变量的值。大概就是这样的。



根据题目，我们之前所写的代码大多数是如下这样的

```javascript
let a=1;
let b=2;
a=a+b;
b=a-b;
a=a-b
console.log(a);
console.log(b);
```

结果可得：a=2，b=1，a，b两个的值已经进行交换了。



但是学了解构赋值这篇博客的内容的话，我们换一种方法来解答这个题目，一种非常舒服、直观的方法。

```javascript
let a = 1;
let b = 2;
[a,b]=[b,a];
console.log(a);
console.log(b);
```

同样得出的结果和上面的一样，a=2，b=1，两个数也进行了交换，但是这种方法比较舒服啊！



##### 2、从函数返回多个值

我们知道，一般从return的时候都是返回一个值的，如果有需要返回多个值的话，一般返回一个对象或者数组就可以了，但是返回来之后取值稍微有点麻烦，利用解构赋值的话就会容易很多。



```javascript
//  返回数组
function splitArray() {
    return [1,2,3]
}
let [a,b,c]=splitArray();
console.log(a);
console.log(b);
console.log(c);

//  返回对象
function splitObj() {
    return{
        x:1,
        y:2,
    }
}
let {x,y}=splitObj();
console.log(x);
console.log(y);
```

**注意：**

>  返回对象的时候，接收的值一定要和返回值的键一致，否则取到的值为undefined



##### 3、函数参数的定义

解构赋值可以很方便的将一组参数和变量名对应起来

```javascript
function foo([x,y,z]) {
    console.log(x+','+y+','+z);
}
foo([1,2,3])
function bar({a,b,c}) {
    console.log(a+','+b+','+c);
}
bar({a:1,c:2,b:10})
```

在bar函数传入参数的时候，我们将顺序打乱传入，但是在解构赋值中，参数名始终和参数值将对应。



##### 4、提取JSON数据

解构赋值对提取JSON对象中的数据，尤其有用，我们一起来看下

```javascript
let obj={
    name:'杨戬',
    age:18,
    sex:'男'
}
let {name,age,sex}=obj;
console.log(name);	//	杨戬
console.log(age);	//	18
console.log(sex);	//	男
```



##### 5、函数参数的默认值

这个用途应该在jQuery扩展插件的时候用的比较多，一般都是根据是否有无参数来指定一些默认值

```javascript
jQuery.ajax = function (url, {
  async = true,
  beforeSend = function () {},
  cache = true,
  complete = function () {},
  crossDomain = false,
  global = true,
  // ... more config
} = {}) {
  // ... do stuff
};
```

指定参数的默认值，就避免了在函数体内部再写 var foo=config.foo||'default foo'这样的语句。



##### 6、遍历Map结构

关于Map这个数据类型，是ES6新增的用来存储数据的结构。这里不过多的进行介绍，后面的文章会有过涉及。



###### 获取键和值

```javascript
const  map=new Map();
map.set('a',10);
map.set('b',20);
map.set('c',30);
for (let [key,value] of map){
    console.log(key+":"+value)
}
```



###### 获取全部的键

```javascript
const  map=new Map();
map.set('a',10);
map.set('b',20);
map.set('c',30);

for (let [key] of map){
    console.log(key)
}
for (let key of map.keys()){
    console.log(key);
}
```



###### 获取全部的值

```javascript
const  map=new Map();
map.set('a',10);
map.set('b',20);
map.set('c',30);

for (let [,value] of map){
    console.log(value)
}
for (let value of map.values()){
    console.log(value);
}
```



##### 7、输入模块的指定方法

这个就比较常用了，尤其是模块化开发的时候，经常需要从某个模块中导入指定的方法。

```javascript
import {aa} from "loading"
```

这种导入非常的清晰明了，模块化开发中经常会使用到。



**参考链接：**

[https://es6.ruanyifeng.com/](ES6教程)



#### 结尾

如果觉得本篇文章对您有用的话，麻烦您给笔者点亮那个点赞按钮。
![](https://s1.ax1x.com/2020/03/23/8oGjfA.th.jpg)

对于杨戬这个暖男来说：**真的非常有用**，您的支持就是我前进的动力，我们下篇文章见。

**作者：** 二郎神杨戬|杨戬

> 原创不易，请勿白嫖。
> 二郎神杨戬，一个在互联网前端苟且偷生的小白一枚，专注于前端开发，善于技术分享。
> 如需转载，请联系作者或者保留原文链接，微信公众号搜索二郎神杨戬。

<img src="https://s1.ax1x.com/2020/05/04/Y9LspR.png" />

