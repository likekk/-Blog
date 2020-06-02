> 点赞再看、养成习惯。
>
> 寄语：长风破浪会有时，直挂云帆济沧海。
> 本文已收录至[https://github.com/likekk/-Blog](https://github.com/likekk/-Blog)欢迎大家star :smile::smile: :smile: ,共同学习，共同进步。如果文章有错误的地方，欢迎大家指出。后期将在将GitHub上规划前端学习的路线和资源分享。



### 前言

通过上一章的学习，我们已经对SpringBoot有简单的入门，接下来我们深入学习一下SpringBoot，我们知道任何一个网站的数据大多数都是动态的，也就是说数据是从数据库提取出来的，而非静态数据，那么我们接下来就是要连接数据库，现在我们经常使用的数据库的种类可以大致分为两种，关系型数据库和非关系型数据库。

- MySQL数据库、Oracle数据库SQL Server数据库等都是关系型数据库
- Redis、Mongodb等等都是非关系型数据库



### 本章目标

- 使用SpringBoot和MyBatis通过注解的方式操作数据库

- 使用SpringBoot和MyBatis通过XML配置文件的方式操作数据库



### 项目搭建

1.打开idea,选择Create New Project

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312090509245-1517928700.png)



2.选择Spring Initializer,然后点击Next

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312090600097-327934830.png)



3.填写组织，坐标等信息，然后点击Next

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312090802474-2084886416.png)



4.选择依赖Web，然后勾选Web,之后一直Next下去，直到项目构建完成。

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312090925865-1411526045.png)



5.项目结构搭好之后，我们新建一些目录分为控制层，服务层，数据访问层，实体层，完整结构如下:

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312091518447-1827290950.png)



6.由于我们要使用MyBatis操作数据库，所以需要添加一些依赖，完整的pom.xml文件如下:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.3.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.demo02</groupId>
    <artifactId>demo_02</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>demo_02</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--mybatis-spring适配器-->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>1.1.1</version>
        </dependency>
        <!--mysql驱动包-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.30</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```



### 数据库相关

1.接下来我们需要新建数据库以及生成实体，数据的建立我就不重复多说了，说一下使用idea快速生成实体(Product)，数据库的sql脚本如下:

```sql
#创建商品信息表
create  table product
(
    pid int primary key not null auto_increment COMMENT"商品编号",
    pname varchar(50) COMMENT"商品名称",
    pprice DECIMAL(10,2) COMMENT"商品价格",
    ptime varchar(50) COMMENT"入库时间",
    pcount int COMMENT"库存",
    pstatus int COMMENT"商品状态" #0 代表下架，1代表上架
)COMMENT"商品信息表"

insert into product(pname,pprice,ptime,pcount,pstatus)VALUES
("苹果",11,"2019-10-1",11,1)

SELECT * from product
```



![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312092343302-115961189.png)



![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312092424313-1491275178.png)





![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312092608771-1620169530.png)



2.Database表示要连接的数据库名称，User表示用户名称，Password表示密码，然后点击Ok,然后选择你要生成实体的目录，生成完成之后基本结构就搭建好了。

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312092859642-645455593.png)

3.Product实体代码如下

```java
package com.ssm.entity;
/*
* 商品实体类
* */
public class Product {

  private long pid;//编号
  private String pname;//名称
  private double pprice;//价格
  private String ptime;//入库时间
  private long pcount;//数量
  private long pstatus;//状态
  //无参构造方法
  public Product() {}
  //带参构造方法
  public Product(long pid, String pname, double pprice, String ptime, long pcount, long pstatus) {
    this.pid = pid;
    this.pname = pname;
    this.pprice = pprice;
    this.ptime = ptime;
    this.pcount = pcount;
    this.pstatus = pstatus;
  }

  public long getPid() {
    return pid;
  }

  public void setPid(long pid) {
    this.pid = pid;
  }


  public String getPname() {
    return pname;
  }

  public void setPname(String pname) {
    this.pname = pname;
  }


  public double getPprice() {
    return pprice;
  }

  public void setPprice(double pprice) {
    this.pprice = pprice;
  }


  public String getPtime() {
    return ptime;
  }

  public void setPtime(String ptime) {
    this.ptime = ptime;
  }


  public long getPcount() {
    return pcount;
  }

  public void setPcount(long pcount) {
    this.pcount = pcount;
  }


  public long getPstatus() {
    return pstatus;
  }

  public void setPstatus(long pstatus) {
    this.pstatus = pstatus;
  }

  @Override
  public String toString() {
    return "Product{" +
            "pid=" + pid +
            ", pname='" + pname + '\'' +
            ", pprice=" + pprice +
            ", ptime='" + ptime + '\'' +
            ", pcount=" + pcount +
            ", pstatus=" + pstatus +
            '}';
  }
}
```



### SpringBoot整合MyBatis基于注解

1.接下来，我们就需要配置一下连接数据库的配置文件，在application.xml中进行配置，applicaion.xml文件如下:

```xml
#连接数据库的驱动
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
#连接数据库的url
spring.datasource.url=jdbc:mysql://localhost:3306/ssm?characterEncoding=utf-8
#用户名
spring.datasource.username=root
#密码
spring.datasource.password=123456
```

2.我们现在就可以操作数据库了，编写ProductDao、ProductService、ProductImple、ProductController以及配置SpringBoot主程序。

**注意：**

> 由于我们新建的包不是和SpringBoot主程序同级目录，所以无法扫描到。项目启动时，只有@SpringBootApplication 所在的包下面才能被扫描到，启动类是MainApplication.java, 也就是MainApplication.java类所在的这个包，而其他的controller和service以及mapper在其他的包里，所以并没有被扫描。所以我们需要配置一下。



ProductDao文件如下：

```java
package com.ssm.dao;
import com.ssm.entity.Product;
import org.apache.ibatis.annotations.Select;
import java.util.List;
public interface ProductDao {
    @Select("select * from product")
    List<Product> findAllProduct();
}
```



ProductService文件如下:

```java
package com.ssm.service;
import com.ssm.entity.Product;
import java.util.List;
public interface ProductService {
    List<Product> findAllProduct();
}
```



ProductImple文件如下：

```java
package com.ssm.service.imple;

import com.ssm.dao.ProductDao;
import com.ssm.entity.Product;
import com.ssm.service.ProductService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import java.util.List;
@Service
public class ProductImple implements ProductService {
    @Autowired
    private ProductDao productDao;
    @Override
    public List<Product> findAllProduct() {
        return productDao.findAllProduct();
    }
}
```



ProductController文件如下：

```java
package com.ssm.controller;

import com.ssm.entity.Product;
import com.ssm.service.ProductService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import java.util.List;
@RestController
public class ProductController {
    @Autowired
    private ProductService productService;
    //查询全部的商品信息
    @GetMapping("/product")
    public List<Product> findAllProduct(){
        return  productService.findAllProduct();
    }
}
```



SpringBoot主程序文件如下：

```java
package com.demo02.demo_02;
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.ComponentScan;
@SpringBootApplication
@ComponentScan(basePackages = {"com.ssm.controller","com.ssm.service"})
@MapperScan(basePackages = {"com.ssm.dao"})
public class Demo02Application {

    public static void main(String[] args) {
        SpringApplication.run(Demo02Application.class, args);
    }

}
```

点击运行，在地址栏输入localhost:8080/product，出现如下结果，那么恭喜您

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312100206625-459670277.png)



### SpringBoot整合MyBatis基于XML配置文件



1.我们现在通过第二种方式操作数据库，我们先将application.xml中的配置文件全部注释，然后新建applicaion.yml,为什么要使用这种格式呢？因为这种方式方便简洁，官方也推荐我们使用这种类型，这是一些的相关格式：

```xml
server:
   port: 8801
eureka:
   client:
     registerWithEureka: false
     fetchRegistry: false
     serviceUrl:
      defaultZone: http://localhost:8801/eureka/
```



2.applicaion.yml配置如下:

```xml
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url:  jdbc:mysql://localhost:3306/ssm?characterEncoding=utf-8
    username: root
    password: 123456
mybatis:
  typeAliasesPackage: com.ssm.entity
  mapperLocations:  classpath:mapper/*Mapper.xml
```



3.我们要通过xml的格式操作数据库也就是我们需要写Mapper.xml文件，在src/main/resources新建Mapper文件夹，然后新建ProductMapper.xml。

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312103738938-1638596898.png)



4.ProductMapper.xml文件如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.ssm.dao.ProductDao">
    <!--查询全部商品信息-->
    <select id="findAllProduct" resultType="product">
        select  * from product
    </select>
</mapper>
```



5.ProductDao文件如下：

```java
package com.ssm.dao;
import com.ssm.entity.Product;
import org.apache.ibatis.annotations.Select;
import java.util.List;
public interface ProductDao {
//    @Select("select * from product")
    List<Product> findAllProduct();
}
```



6.ProductService文件如下：

```java
package com.ssm.service;
import com.ssm.entity.Product;
import java.util.List;
public interface ProductService {
    List<Product> findAllProduct();
}
```



7.ProductImple文件如下：

```java
package com.ssm.service.imple;
import com.ssm.dao.ProductDao;
import com.ssm.entity.Product;
import com.ssm.service.ProductService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import java.util.List;
@Service
public class ProductImple implements ProductService {
    @Autowired
    private ProductDao productDao;
    @Override
    public List<Product> findAllProduct() {
        return productDao.findAllProduct();
    }
}
```



8.ProductController文件如下：

```java
package com.ssm.controller;
import com.ssm.entity.Product;
import com.ssm.service.ProductService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import java.util.List;
@RestController
public class ProductController {
    @Autowired
    private ProductService productService;
    //查询全部的商品信息
    @GetMapping("/product")
    public List<Product> findAllProduct(){
        return  productService.findAllProduct();
    }
}
```



9.SpringBoot主程序文件如下：

```java
package com.demo02.demo_02;
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.ComponentScan;
@SpringBootApplication
@ComponentScan(basePackages = {"com.ssm.controller","com.ssm.service"})
@MapperScan(basePackages = {"com.ssm.dao"})
public class Demo02Application {
    public static void main(String[] args) {
        SpringApplication.run(Demo02Application.class, args);
    }

}
```



10.运行，结果和之前的一样

![](https://img2018.cnblogs.com/blog/1475945/201903/1475945-20190312104036196-352404249.png)

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

