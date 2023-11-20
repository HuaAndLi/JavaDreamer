[TOC]



# 简介

第一天学习笔记

# 学什么 怎么学



编程重点学的是思维，代码仅仅是工具，思维的一种体现方式。**一定要有编程思维！**

先听 后学 然后输出。

每一个代码都要可以脱离书本和视频，自己写出来。

学会整理笔记。



# Java基础目录

- 计算机基础知识
- Java基础语法
- 面向对象
- API
- 集合
- 学生管理系统

# 计算机基础知识

## 计算机简介

计算机发展史自己去了解

## 数据存储和运算

底层一系列电路断开，连接（没有电，有电），代表0，1。

1B=8bit

## 数据运算

二进制运算。

程序员计算器。



## 常见进制

[【精选】五、进制和计算机中数据表示形式（包括码制）_计算机中各进制数形式如何表示-CSDN博客](https://blog.csdn.net/qq_38367575/article/details/113405558)

二进制，八进制，十进制。

存储2进制，编码默认10进制。

```java
int a = 100;//10进制
int b = 0b100;//2进制
int c = 0100;//8进制   09会报错
int d = 0x100;//16进制
```



## 硬件和软件

硬件（冯诺依曼）

- cpu = 运算器和控制器 （大脑）

- 输入设备（鼠标键盘）

- 存储器（硬盘永久，内存临时）

- 输出设备（显示器，打印机）

软件

- 系统软件
  - windows
  - ios
  - linux
- 应用软件
  - qq(C/S)
  - 微信(C/S)
  - 浏览器（B/S）
  - 微信小程序（B/S）



## 计算机语言

人与计算机之间交流方式

- 机器语言

  ​		0/1代码，打孔带

- 汇编

  ​		转为英文单词

  ​		例如：add 1,2

  ​		需要转为0/1代码

- 高级语言

  ​		使用普通英语编写，通过编译器翻译类似汇编语言的指令，再由计算机执行。



## 人机交互方式

- 图像化界面
- 命令行方式
  - [一、Windows常用命令_张丁花的博客-CSDN博客](https://blog.csdn.net/qq_38367575/article/details/113333691)


## Path环境变量

Path会记录一些程序所在的完整路径

需要运行一个程序，但是没有写完成路径，获取path配置的路径下找。

开发软件配置Path方便。



# Java介绍与搭建环境

## 背景

oak -> Java  自己去了解

[【精选】二、JAVA的简单介绍及jdk安装环境和配置_请描述安装配置jdk_张丁花的博客-CSDN博客](https://blog.csdn.net/qq_38367575/article/details/113355244)



## 跨平台

平台：操作系统

跨平台： 所有操作系统都可以运行

原理：系统装了JVM



## JDK、JRE、JVM

JVM: Java虚拟机

JRE: Java运行时环境，包含JVM，核心类库

JDK: Java开发工具包，包含JRE、常用开发工具包（javac编译工具，Java运行工具）

## JDK安装

[【精选】二、JAVA的简单介绍及jdk安装环境和配置_请描述安装配置jdk_张丁花的博客-CSDN博客](https://blog.csdn.net/qq_38367575/article/details/113355244)



## HelloWorld程序

记事本编写：HelloWorld.java

```java
public class HelloWorld{

	public static void main(String[] args){
		System.out.println("HelloWorld");

	}
}
```

Dos窗口输入

```shell
javac HelloWorld.java
java HelloWorld
```



## 配置Java环境变量

自己搜

##  IDEA

现在主流的Java开发集成工具，自己学习。

## 注释

[三、java中的关键字和标识符、注释(包括提取注释文档)_java关键词提取和标注-CSDN博客](https://blog.csdn.net/qq_38367575/article/details/113404368)

对程序进行解释

- 单行注释 //
- 多行注释 /*  */
- 文档注释/**   */
- TODO: 待完成的任务标注

