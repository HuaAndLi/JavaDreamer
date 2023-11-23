# 填空题

### 题目一

说出如下结果：

```java
String s1 = "abc";
String s2 = "abc";

System.out.println(s1 == s2);
```

答案：用双引号，指向字符串常量池中的同一个元素。true



### 题目二

说出如下结果：

```java
String s1 = "abc";
String s2 = new String("abc");

System.out.println(s1 == s2);
```

答案：s1在字符串常量池中，s2在堆中。false

### 题目三

说出如下结果：

```java
String s1 = "abc";
String s2 = "ab";
String s3 = s2 + "c";

System.out.println(s1 == s3);
```

答案：s1在字符串常量池中，s2在字符串常量池中，s3通过StringBuilder连接。false

### 题目四

说出如下结果：

```java
String s1 = "abc";
String s2 = "a" + "b" + "c";

System.out.println(s1 == s2);
```

答案：s1在字符串常量池中，s2编译期间Java存在常量优化机制，等同于s2="abc",由于字符串常量池中有了，直接引用。true

