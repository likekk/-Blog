> 点赞再看、养成习惯。

> 寄语：长风破浪会有时，直挂云帆济沧海。
> 本文已收录至[https://github.com/likekk/-Blog](https://github.com/likekk/-Blog)欢迎大家star :smile::smile: :smile: ,共同学习，共同进步。如果文章有错误的地方，欢迎大家指出。后期将在将GitHub上规划前端学习的路线和资源分享。



### 前言

在没有SpringBoot之前，我们搭建的是SSM(SpingMVC+Spring+Mybatis)项目，搭建SSM项目的时候，我们要经过一系列的繁琐配置，例如：application,web.xml，spring-servlet等等的配置信息。如果我们这些配置出现一点点的错误。那么面临的就是寻找一大堆的Bug,而且还出现一些我们看难以看懂的异常，对于English不好的同志来说，这是内伤。那么SpringBoot到底解决了什么问题呢？简单来说，SpringBoot主要简化了我们的配置操作，将那些我们需要配置的东西封装好了，我们拿来即用，它的好处如下：

- 创建独立的Spring应用程序

- 嵌入的Tomcat，无需部署WAR文件
- 简化Maven配置
- 自动配置Spring
- 提供生产就绪型功能，如指标，健康检查和外部配置
- 绝对没有代码生成并且对XML也没有配置要求

### 项目搭建

1.新建一个SpringBoot项目，打开开发工具idea，选择Create New Project

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310214820869-35621724.png)



2.选择Spring Initializr,点击Next

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310214846192-437915289.png)



3.这里有些关于maven的知识，由于博主暂时没有写关于Maven的博客，希望各位能够谅解，博主在今后的时间会补上，直接点击next

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310215441614-1456677962.png)



4.这一部分的界面有许多依赖，当我们后期的开发中需要用到的时候可以选择，现在的话我们就什么都不选，直接点击Next

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310215600409-2024497185.png)



5.直接点击finish,一个简单的SpringBoot项目就完成了

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310215745136-1650953553.png)



6.简单的SpringBoot项目结构如下

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310220811932-1869820329.png)



7.每一个SpringBoot项目都有一个主程序，直接启动，这里我们不需要配置Tomcat，主程序结构如下

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310221136934-277050216.png)



8.我们直接可以运行项目，SpringBoot默认端口是8080端口，后期可以通过配置文件进行修改，在地址栏输入localhost:8080

[![](https://s1.ax1x.com/2020/06/01/tJT4Mt.jpg)](https://imgchr.com/i/tJT4Mt)

此时的话什么都没有，别急，我们新建一个控制器，然后添加一些静态数据模拟数据库，在添加控制器之间我们需要添加一些依赖，这个依赖属于web部分，在最开始直接依赖那一部分我们没有选择，所以我们就主动添加依赖。

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```



9.目录结构和控制器代码如下

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310222533684-1963818821.png)



```java
package com.ssm.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.HashMap;
import java.util.Map;

@RestController
public class IndexController {
    @RequestMapping("/index")
    public Map index(){
        Map map=new HashMap();
        map.put("name","一只流浪的KK");
        map.put("type","公猿");
        map.put("sex","male");
        return  map;
    }
}
```



10.我们现在一切准备就绪，点击运行，然后在地址栏输入localhost:8080/index，此时界面表示没有找到。

![](https://s1.ax1x.com/2020/06/01/tJT4Mt.jpg)

别急，还有特别重要的一步没有写完，我发现许多博主都没有写到，在这里我就将他们的坑填上。

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310222826428-99276761.png)



11.各位是否还记得我们之前所说的每一个SpringBoot项目都有一个主程序入口，现在我们就去主程序入口配置一下。新增一个注解，后期的博客我将会详细讲解每一个注解的作用。在这里就不一一介绍了。

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190310223250849-375671161.png)



12.此时，我们在重新启动项目，然后在地址栏输入localhost:8080/index,如果出现如下结果，那么恭喜各位已经成功完成了第一个SpringBoot项目。此时我们看到已经可以显示数据了。

![](https://s1.ax1x.com/2020/06/01/tJ7LTO.jpg)



### @RestControllerVS@Controller

- @RestController是@Controller和@ResponseBody的结合，当在一个控制器里标注了@RestController的时候，那么整个控制器的返回值都是json，而无法返回视图，如果需要返回视图可以使用@Controller

- 当使用@Controller的时候，我们一般返回视图，如果需要返回json，那么请在需要返回json的方法上方标注@ResponseBody，就可以返回json了。



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