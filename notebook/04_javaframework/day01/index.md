[TOC]



# 简介

第1天学习笔记



# Spring

主要学IOC和DI

IOC控制反转，把创建Bean的控制权交给Spring的IOC容器，由自己new交给Spring IOC来实例化。

DI ，Spring IOC可以把依赖进行绑定。

解耦。

## IoC入门案例（XML版）

1.导入Spring坐标

```xml
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
```

2.定义Spring管理的类（接口）

源码联系作者。

3.创建Spring配置文件,添加如下代码

```xml
<bean class="com.itheima.dao.impl.BookDaoImpl" id="bookDao"></bean>
```

4.使用IOC容器获取对象

```java
//目标:要在IOC容器中获取id=bookDao的对象
    @Test
    public void test01() {
        //1.使用spring加载application-quickstart.xml，帮助我们将xml中的创建的对象放到IOC容器中
        ClassPathXmlApplicationContext ctx = new ClassPathXmlApplicationContext("application-quickstart.xml");
        //2.使用IOC容器获取ID=bookDao的对象
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        //3.调用对象中的save()方法
        bookDao.save();
        //4.关闭容器
        ctx.close();
    }
```

## DI入门案例（XML版）

1.把直接new的去掉。

2.设置set方法

3.配置service和dao之间的关系

```xml
<bean class="com.itheima.service.impl.BookServiceImpl" id="bookService">
        <property name="bookDao" ref="bookDao"/>
    </bean>
```

4.通过IOC容器获取service对象

```java
    //目标:要在IOC容器中获取id=bookService的对象,进行DI
    @Test
    public void test02() {
        //1.使用spring加载application-quickstart.xml，帮助我们将xml中的创建的对象放到IOC容器中
        ClassPathXmlApplicationContext ctx = new ClassPathXmlApplicationContext("application-quickstart.xml");
        //2.使用IOC容器获取ID=bookService的对象
        BookService bookService = (BookService) ctx.getBean("bookService");
        //3.调用对象中的save()方法
        bookService.save();
        //4.关闭容器
        ctx.close();
    }
```

其他代码可联系作者。

## bean的作用范围

## bean的生命周期



