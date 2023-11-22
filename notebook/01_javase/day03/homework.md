# 选择题

### 题目1(单选):

**下列属于正确的自增自减运算符的是( A )**

#### 选项 :

​	A. ++和--

​	B.+和-

​	C.+++和---

​	D.-和/



### 题目2(单选):

**下列代码的运行结果是( A  )**

```java
int x = 10;
int y = x++;   	
int z = ++x; 	
System.out.println(x);
System.out.println(y);
System.out.println(z);
```

#### 选项 :

​	A. 12 10 12

​	B. 10 11 12

​	C. 11 11 10 

​	D. 12 10 11



### 题目3(单选):

**下列关于自减运算符描述正确的是(  B )**

#### 选项 :

​	A. --可以使用在常量中

​	B.--如果放在变量的后面，是先参与操作，然后再自减

​	C.--如果放在变量的前面，是先参与操作，然后再自增

​	D.--如果放在变量的后面，是先执行自减，然后再参与操作



### 题目4(单选):

**下列代码的运行结果是( D )**

```java
public class Test {
    public static void main(String[] args) {
        double a = 12.3;
        int b = a;
        System.out.println(b);
    }
}
```

#### 选项 :

​	A. 12

​	B. 12.3

​	C. 12.0

​	D. 编译错误



### 题目5(单选):

**下列代码的运行结果是( C  )**

```java
public class Test {
    public static void main(String[] args) {
        int a = 10;
        double b = 12.3;
        a += b;
        System.out.println(a);
    }
}
```

#### 选项 :

​	A.  编译错误, 没有做强转

​	B.  22.3

​	C.  22

​	D.  22.0



### 题目6(单选):

**下列代码的运行结果是(  B )**

```java
public class Test {
    public static void main(String[] args) {
        int a = 1;
        int b = 2;

        boolean result = a++ > 3 && --b < 4;

        System.out.println(a);
        System.out.println(b);
        System.out.println(result);
    }
}
```



#### 选项 :

​	A.  1  2  false

​	B.  2  2  false

​	C.  1  2  true

​	D.  2  2  true



### 题目7(多选):

**下列对于逻辑赋值运算符特点描述正确的是( ABCD )**

#### 选项 :

​	A.  &符号遇false则false

​	B.  |符号遇true则true

​	C.  && 具有短路效果, 左边为false, 右边不执行

​	D.  || 具有短路效果, 左边为true, 右边不执行





### 题目8(多选):

**下列关于if语句的描述, 说法正确的是( BC )**

#### 选项 :

​	A.  if 语句的 () 和 {} 之间可以编写分号,  对程序没有任何影响

​	B.  if 语句的 {} 中如果只有一条语句, {} 可以省略不写

​	C.  if 语句的 () 中, 最终产生的是一个boolean类型结果, 根据这个结果决定程序的走向

​	D.  if 语句的 {} 无论何时都不能省略



### 题目9(单选):

**下列代码的运行结果是( B  )**

```java
public class Test {
    public static void main(String[] args) {
        int a = 1;
        int b = 1;
        int c = 0;

        if (a > b) {
            c = 10;
        }else if(a < b){
            c = 20;
        }

        System.out.println(c);
    }
}
```

#### 选项 :

​	A.  编译错误, 缺少最后的else代码块

​	B.  0

​	C. 10

​	D. 20



### 题目10(单选):

**键盘录入数据为200,  下列代码的运行结果是( C )**

```java
public class Test {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入成绩:");
        int score = sc.nextInt();

        if (score >= 0 && score <= 100) {
            if (score >= 95 && score <= 100) {
                System.out.println("山地自行车一辆");
            } else if (score >= 90 && score <= 94) {
                System.out.println("游乐场玩一次");
            } else if (score >= 80 && score <= 89) {
                System.out.println("变形金刚玩具一个");
            } else {
                System.out.println("挨顿揍");
            }
        }
    }
}
```

#### 选项 :

​	A. 编译错误

​	B. 挨顿揍

​	C. 程序正常运行, 但是没有任何结果输出

​	D. 以上说法都不对



# 编程题

### 题目1（加强训练）

通过键盘输入一个年龄，使用if语句对年龄进行判断。

如果年龄大于等于18，则输出：恭喜，您已经成年了！

#### 训练目标

能够使用if语句的第一种格式

#### 训练提示

1、编写一个java文件

2、编写类和main方法

3、通过键盘输入一个数字

4、对数字进行判断

#### 参考方案

键盘录入Scanner、if语句、关系运算符

#### 操作步骤

1、编写一个文件，名称为：Test01.java

2、编写定义类的代码

3、编写main方法

4、通过键盘输入一个数字，代表年龄

5、通过if语句进行判断

​		如果年龄大于等于18，则输出：恭喜，您已经成年了！

#### 参考答案

```java
import java.util.Scanner;

public class Test01 {
    public static void main(String[] args) {
        //通过键盘录入数字
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个年龄：");
        int age = sc.nextInt();
        
        //使用if语句进行判断
        if( age >= 18 ) {
            System.out.println("恭喜，您已经成年了！");
        }
    }
}
```





### 题目2（加强训练）

键盘录入学生考试成绩，判断学生等级:

90-100   优秀

80-89    好

70-79    良

60-69    及格

60以下  不及格



#### 训练目标

能够熟练运用 if 语句

#### 训练提示

1、编写一个java文件

2、编写类和main方法

3、通过键盘输入一个成绩

4、因为是多条件判断，所以使用 if..else..if 语句

5、注意错误值的判断

#### 参考方案

键盘录入Scanner、if语句、关系运算符、逻辑运算符

#### 操作步骤

1、编写一个文件，名称为：Test02.java

2、编写定义类的代码

3、编写main方法

4、通过键盘输入一个数字，代表成绩

5、通过 if...else...if 语句进行判断



#### 参考答案

```java
public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    System.out.println("请输入成绩:");
    // 1. 键盘录入学生成绩
    int score = sc.nextInt();

    // 2. 判断成绩是否在0-100之间
    if (score >= 0 && score <= 100) {

        // 3. 根据成绩所在的区间判断, 程序给出不同的结果
        if (score >= 90 && score <= 100) {
            System.out.println("优秀");
        } else if (score >= 80 && score <= 89) {
            System.out.println("好");
        } else if (score >= 70 && score <= 79) {
            System.out.println("良");
        } else if (score >= 60 && score <= 69) {
            System.out.println("及格");
        } else {
            System.out.println("不及格");
        }

    } else {
        System.out.println("您的输入有误, 请检查成绩是否在0~100之间");
    }

  }
}
```