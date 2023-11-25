[TOC]



# 简介

第4天学习笔记

# 日期与时间

## Date

[十三、JAVA中的Date和SimpleDateFormat](https://blog.csdn.net/qq_38367575/article/details/120238744)

## SimpleDateFormat

[十三、JAVA中的Date和SimpleDateFormat](https://blog.csdn.net/qq_38367575/article/details/120238744)

## Calendar

抽象类，代表系统日历对象

# JDK8 新增日期类 

了解即可



# 包装类

[十二、JAVA中的包装类](https://blog.csdn.net/qq_38367575/article/details/120238343)

# 正则表达式

自己搜一下

# Arrays工具类

[八、java中的方法和数组（包括方法的重载、Arrays工具类的使用、数组缩容和扩容）](https://blog.csdn.net/qq_38367575/article/details/120187313)

# Lambda表达式

JDK8 新的语法形式

作用：简化匿名内部类的写法

```java
package com.itheima.d9_lambda;

/**
 * 目标：Lambda表达式的格式和使用前提。
 */
public class LambdaDemo1 {
    public static void main(String[] args) {
        Animal a = new Animal() {
            @Override
            public void run() {
                System.out.println("匿名test");
            }
        };
        a.run();
        System.out.println("----Lambda简化------");
        //错误必须是接口，而且只有一个抽象方法。
//        Animal animal = ()->{
//            System.out.println();
//        };
        System.out.println("----------");
        go(new Swimming() {
            @Override
            public void swim() {
                System.out.println("游泳");
            }
        });
        go(() -> {
            System.out.println("游泳");
        });

    }

    public static void go(Swimming s) {
        System.out.println("开始。。");
        s.swim();
        System.out.println("结束。。");
    }
}

interface Swimming {
    void swim();
}

abstract class Animal {
    public abstract void run();
}

```



