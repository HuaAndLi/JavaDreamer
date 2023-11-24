[TOC]



# 简介

第2天学习笔记

# 包

```java
package cn.zxh.d1_package;

import cn.zxh.d1_package.demo1.Animal;

public class Test {
    public static void main(String[] args) {
        // 1、相同包下的类可以互相访问
        Student.inAddr();
        // 2、不同的包下的类，必须进行导包才可以使用
        System.out.println(Animal.name);
        // 3、相同类，默认只能导入一个，想使用另一个类，必须是 包名+类名(全类名) 访问
        System.out.println(cn.zxh.d1_package.demo2.Animal.name);

    }
}

```

# 权限修饰符

```java
package cn.zxh.d2_modifier.dyl;

public class Fu {
    //1.private只能本类中访问
    private void show1() {
        System.out.println("private");
    }

    //2.缺省：本类，同一个包下的类中。
    void show2() {
        System.out.println("缺省");
    }


    //3.protected:本类，同一个包下的类中，其他包下的子类
    protected void show3() {
        System.out.println("protected");
    }

    //4.任何地方都可以
    public void show4() {
        System.out.println("public");
    }

    public static void main(String[] args) {
        //创建FU的对象，测试看有哪些方法可以使用
        Fu f = new Fu();
        f.show1();
        f.show2();
        f.show3();
        f.show4();
    }
}
```



# final关键字

```java
package cn.zxh.d3_final;

/**
 * 目标：明白final一些基本语法知识
 */
public class Test {
    //final修饰静态成员变量：称为常量
    //常量：应该是static final修饰的成员变量称为常量，其值不变
    //常量的名称，建议全部大写，多个单词用下划线连接
    public static final String SCHOOL_NAME = "国科大";
    public static final String SCHOOL_NAME2;

    static {
        SCHOOL_NAME2 = "3";
//        SCHOOL_NAME2 = "3";//第二次赋值，报错
    }

    //final修饰的实例成员变量,其值不能被改变（鸡肋语法没有用意义）
    private final String name = "zxh";

    public static void main(String[] args) {
        //3.final修饰变量，有且仅能被赋值一次
        /**
         Java的变量是怎么分类：
         1.成员变量
         静态成员变量
         实例成员变量
         2.局部变量
         方法内部的，方法的形参，for循环的i
         */

        final int age = 30;
//        age = 24; //第二次赋值，报错
        System.out.println(age);

        final double rate = 3.14;
//        rate = 24; //第二次赋值，报错

        final int[] arr = {12,23,343};
//        arr  = {23,32};//第二次赋值，报错
        arr[2] = 3;

        //保护数据不被修改
        buy(0.3);

//        schoolName = "33";//第二次赋值，报错

        Test t = new Test();
//        t.name = "s";//第二次赋值，报错
    }


    public static void buy(final double z) {
//        z = 0.1;//第二次赋值，报错
    }
}

//1.final修饰类，类不能被继承了
//final class Animal {
//}
//class Cat extends Animal {
//}

//2.final修饰方法，方法不能重写了
//class Animal {
//    public final void run() {
//    }
//}
//class Dog extends Animal{
//    @Override
//    public void run() {
//    }
//}


```

# 常量

```java
package cn.zxh.d4_constant;

/**
 * 目标：学会常量的使用，并理解常量
 */
public class ConstantDemo1 {
    // 系统的配置信息
    public static final String SCHOOL_NAME = "国科大";
    public static final String LOGIN_NAME = "admin";
    public static final String PASS_WORD = "123456";

    public static void main(String[] args) {
        System.out.println(SCHOOL_NAME);
        System.out.println(SCHOOL_NAME);
        System.out.println(SCHOOL_NAME);
        System.out.println(SCHOOL_NAME);
        System.out.println(SCHOOL_NAME);
        System.out.println(SCHOOL_NAME);
        System.out.println(SCHOOL_NAME);
        System.out.println(SCHOOL_NAME);
        System.out.println(SCHOOL_NAME);
    }
}

```

# 枚举

```java
package cn.zxh.d5_enum;

/**
 * 枚举类：认识它
 */
public enum Season {
    // 第一行是枚举类的对象名称。
    SPRING, SUMMER, AUTUMN, WINTER;

}
package cn.zxh.d5_enum;

/**
 * 目标：认识枚举
 */
public class EnumDemo1 {
    public static void main(String[] args) {
        Season s1 = Season.SPRING;
        Season s2 = Season.SUMMER;
        Season s3 = Season.AUTUMN;
        Season s4 = Season.WINTER;

//        Season s5 = new Season();
    }
}

```

# 抽象类

```java
package cn.zxh.d6_abstract_class;

/**
 * 抽象类
 */
public abstract class Animal {
    //抽象方法
    public abstract void run();
}

package cn.zxh.d6_abstract_class;

public class Cat extends Animal{
    @Override
    public void run() {
        System.out.println("猫跑上树");
    }
}


package cn.zxh.d6_abstract_class;

/**
 * 目标：认识抽象类，了解它的基本作用
 */
public class Test {
    public static void main(String[] args) {
        Cat cat =new Cat();
        cat.run();
    }
}

```

# 接口

```java
package cn.zxh.d10_interface;

/**
 * 接口的定义和认识
 */
public interface DataInter {
    //1.常量
//    public static final String LOGIN_NAME = "admin";
//    public static final String PASSWORD = "admin";
    String LOGIN_NAME = "admin";
    String PASSWORD = "admin";

    //2.抽象方法
//    public abstract  void deleteData();
//    public abstract  void queryData();
    // 默认会自动加上 public abstract
    void deleteData();
    void queryData();


}

```



