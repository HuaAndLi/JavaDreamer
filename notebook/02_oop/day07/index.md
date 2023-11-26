[TOC]



# 简介

第7天学习笔记



# 不可变集合

使用Map、Set、List接口直接.of()就可以创建，不能进行任何更改操作。

# Stream流

目的：简化集合和数组的API

**Stream流的获取**

```java
package com.itheima.d2_stream;

import java.util.*;
import java.util.stream.Stream;

/**
     目标：Stream流的获取

     Stream流式思想的核心：
                 是先得到集合或者数组的Stream流（就是一根传送带）
                 然后就用这个Stream流操作集合或者数组的元素。
                 然后用Stream流简化替代集合操作的API.

     集合获取流的API:
         (1) default Stream<E> stream();

     小结：
         集合获取Stream流用: stream();
         数组：Arrays.stream(数组)   /  Stream.of(数组);
 */
public class StreamTest2 {
    public static void main(String[] args) {
        /** --------------------获取Collection系列集合的Stream流-------------------------------   */
        Collection<String> list = new ArrayList<>();
        Stream<String> s1 = list.stream();

        /** --------------------获取Map系列集合的Stream流-------------------------------   */
        Map<String, Integer> maps = new HashMap<>();
        // 键流
        Stream<String> s2 = maps.keySet().stream();
        // 值流
        Stream<Integer> s3 = maps.values().stream();
        // 键值对流（拿整体）
        Stream<Map.Entry<String, Integer>> stream = maps.entrySet().stream();

        /** ---------------------获取数组的Stream流------------------------------   */
        String[] names = {"赵敏","小昭","灭绝","周芷若"};
        // 两种写法的效果是一样的！
        Stream<String> s4 = Arrays.stream(names);
        Stream<String> s5 = Stream.of(names);

    }
}

```

*Stream**流的常用**API*

```java
package com.itheima.d2_stream;

import java.io.Serializable;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.stream.Stream;

/**
     目标：Stream流的常用API
         forEach : 逐一处理(遍历)
         count：统计个数
            -- long count();
         filter : 过滤元素
            -- Stream<T> filter(Predicate<? super T> predicate)
         limit : 取前几个元素
         skip : 跳过前几个
         map : 加工方法
         concat : 合并流。
 */
public class StreamTest3 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("张无忌");
        list.add("周芷若");
        list.add("赵敏");
        list.add("张强");
        list.add("张三丰");
        list.add("张三丰");

        // 1、得到集合获取数组的Stream流对象，再使用其封装的方法
        Stream<String> stream = list.stream();
        // 2、过滤数据
        stream.filter(s -> s.startsWith("张")).filter(s -> s.length() == 3).forEach(a -> System.out.println(a));

        // 3、统计数量
        long size = list.stream().filter(s -> s.startsWith("张")).filter(s -> s.length() == 3).count();
        System.out.println("姓张的人且名字个数是3个的：" + size);

        // 4、取前几个，跳过前几个元素
        list.stream().limit(3).forEach(s -> System.out.println(s));
        list.stream().skip(3).forEach(s -> System.out.println(s));

        // 5、map : 加工方法。
        // 需求：把所有人的名字前面加上一个“黑马的：”
        list.stream().map(s -> "黑马的：" + s).forEach(s -> System.out.println(s));
        // 需求：把学生名称加工成学生对象。
        list.stream().map(name -> new Student(name)).forEach(s -> System.out.println(s));
        // 方法引用（拓展，无需理会）
        list.stream().map(Student::new).forEach(System.out::println);

        // 6、concat : 合并流。
        Stream<String> s1 = list.stream();
        Stream<Integer> s2 = Stream.of(12,123,333);
        //  public static <T> Stream<T> concat(Stream<? extends T> a, Stream<? extends T> b)
        Stream<Object> concat = Stream.concat(s1, s2);
        System.out.println(concat.count());

    }
}

```



# 异常处理

[八、JAVA中的异常和处理和访问权限修饰符](https://blog.csdn.net/qq_38367575/article/details/120206171)

