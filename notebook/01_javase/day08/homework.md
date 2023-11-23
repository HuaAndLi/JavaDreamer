# 单选题

### 题目1(单选): 

**下列信息中包含的内容是类与对象关系的是（ C ） **

选项 :

​	A. 猫和狗 

​	B. 张三同学和李四同学

​	C. 手机和华为P40

​	D. 手机和电脑



------

### 题目2(单选):

**下列代码的运行结果是（ A ）**

```java
public class Student {
    String name;
    int age;
    public void show() {
        System.out.println(name + "，" + age);
    }
}
```

```java
public class Test {
    public static void main(String[] args) {
        Student s = new Student();
        s.show();
        s.name = "赵子龙";
        s.age = 66;
        s.show();
    }
}
```

选项 :

​	A. null，0 

​	    赵子龙，66

​	B. ""，0 

​		"赵子龙"，66

​	C. null，null 

​		"赵子龙"，"66"

​	D. 0，0

​		"赵子龙"，"66"

------

### 题目3(单选): 

**下列关于局部变量和成员变量描述错误的是（ B）** 

选项 :

​	A.  成员变量定义在类中方法外，局部变量定义在方法内。 

​	B.  成员变量和局部变量在整个类中都可以使用

​	C.  成员变量有默认值，局部变量没有默认值，必须先赋值，后使用. 

​	D.  成员变量在堆内存，局部变量在栈内存。

------

### 题目4(单选): 

​	**观察以下代码 , 横线处应该填写的正确代码是（ C ）**

**运行结果是：**

```
键盘敲烂,薪资过万...
```

```java
public class Demo {
    public static void main(String[] args){
       ___________
    }
}
class Student {
    public void study(){
        System.out.println("键盘敲烂,薪资过万...");
    }
}
```

选项 :

​	A.  Student s = new Student();          System.out.println(s.study());

​	B.  Student s = new Student();          void v = s.study();

​	C.  Student s = new Student();          s.study();

​	D.  Student s = new Student();          s.study("键盘敲烂,薪资过万...");

------

### 题目5(单选): 

**观察以下代码 , 在方法中调用变量,输出结果正确的是（ C ） **

```java
public class Demo {
	public static void main(String[] args) {
        Student s = new Student();
        s.name = "老李";
        s.show("老王");
    }
}
class Student {
    String name;
    public void show(String name){
        System.out.println(name);
        System.out.println(this.name);
    }
}
```

选项 :

​	A. 老王 , 老王

​	B. 老李 , 老李

​	C. 老王 , 老李

​	D. 老李 , 老王

------

### 题目6(单选): 

**下列选项关于封装描述错误的为（  A ）** 

选项 :

​	A.  封装指的就是 private

​	B.  封装是面向对象三大特征之一

​	C.  封装隐藏实现细节 , 对外暴露公共的访问方式

​	D.  将代码抽取到方法中 , 是对代码的一种封装体现 , 将属性抽取到类中, 这是对数据的一种封装体现 

------



### 题目7(多选): 

**下列选项中 , 哪些关键字属于权限修饰符 (ABC  )** 

选项 :

​	A.   public 

​	B.   private

​	C:   protected

​	D.   package

------



# 编程题



面向对象

## 题目1（完成）

定义手机类，手机有品牌(brand),价格(price)和颜色(color)三个属性，有打电话call()和sendMessage()两个功能。

请定义出手机类，类中要有空参、有参构造方法，set/get方法。 

定义测试类，在主方法中使用空参构造创建对象，使用set方法赋值。

调用对象的两个功能，打印效果如下：

```
正在使用价格为3998元黑色的小米手机打电话....
正在使用价格为3998元黑色的小米手机发短信....
```

### 训练提示

1. 类中的属性就是成员变量，类中的行为功能就是成员方法。
2. 成员变量要被private修饰。

### 解题方案

### 操作步骤

1. 定义手机类，手机类中定义String类型的品牌，int类型的价格，String类型的颜色，三个成员变量都用privice修饰。
2. 提供空参构造方法和有参构造方法。
3. 提供set/get方法。
4. 编写打电话的成员方法，方法中对成员变量进行使用。
5. 编写发短信的成员方法，方法中对成员变量进行使用。
6. 在测试类中创建手机对象，使用set方法赋值，分别调用各个方法。

### 参考答案

```java
package com.itheima.a;

public class Phone {
    private String brand;

    private Double price;

    private String color;

    public Phone() {
    }

    public Phone(String brand, Double price, String color) {
        this.brand = brand;
        this.price = price;
        this.color = color;
    }


    public void call() {
        System.out.println("正在使用价格为" + this.price + "元" + color + "的" + brand + "手机打电话....");
    }

    public void sendMessage() {
        System.out.println("正在使用价格为" + this.price + "元" + color + "的" + brand + "手机发短信....");
    }

    /**
     * 获取
     *
     * @return brand
     */
    public String getBrand() {
        return brand;
    }

    /**
     * 设置
     *
     * @param brand
     */
    public void setBrand(String brand) {
        this.brand = brand;
    }

    /**
     * 获取
     *
     * @return price
     */
    public Double getPrice() {
        return price;
    }

    /**
     * 设置
     *
     * @param price
     */
    public void setPrice(Double price) {
        this.price = price;
    }

    /**
     * 获取
     *
     * @return color
     */
    public String getColor() {
        return color;
    }

    /**
     * 设置
     *
     * @param color
     */
    public void setColor(String color) {
        this.color = color;
    }

    public String toString() {
        return "Phone{brand = " + brand + ", price = " + price + ", color = " + color + "}";
    }

    public static void main(String[] args) {
        Phone phone = new Phone("小米", 3998.0, "黑色");
        phone.call();
        phone.sendMessage();
    }
}

```

## 题目2（完成）

定义项目经理类Manager。属性：姓名name，工号id，工资salary，奖金bonus。行为：工作work()
定义程序员类Coder。属性：姓名name，工号id，工资salary。行为：工作work()

要求：

​	1.按照以上要求定义Manager类和Coder类,属性要私有,生成空参、有参构造，set和get方法
​	2.定义测试类,在main方法中创建该类的对象并给属性赋值(set方法或有参构造方法)
​	3.调用成员方法,打印格式如下:		

```
调用项目经理中的work方法之后的效果：
工号为123基本工资为15000奖金为6000的项目经理正在努力的做着管理工作,分配任务,检查员工提交上来的代码.....
调用程序员中的work方法之后的效果：
工号为135基本工资为10000的程序员正在努力的写着代码......
```

### 训练提示

1. 类中的属性就是成员变量，类中的行为功能就是成员方法。
2. 成员变量要被private修饰。
3. 在工作work()方法中调用成员变量，输出成员变量的值。

### 解题方案

### 操作步骤

1. 定义项目经理类，定义成员变量，构造方法，set和get方法，work方法，方法中根据打印格式输出id,salary,bonus的值。
2. 定义程序员类，定义成员变量，构造方法，set和get方法，work方法，方法中根据打印格式输出id和salary的值。
3. 在测试类中使用有参构造创建项目经理对象并赋值，调用工作方法打印结果。
4. 在测试类中使用有参构造创建程序员对象并赋值，调用工作方法打印结果。

### 参考答案

```java
package com.itheima.homework;

public class Manager {

    private String name;

    private Integer id;

    private Double salary;

    private Double bonus;

    public void work() {
        System.out.println("工号为" + this.id + "基本工资为" + this.salary + "奖金为" + this.bonus + "的项目经理" + this.name + "正在努力的做着管理工作,分配任务,检查员工提交上来的代码.....");
    }

    public Manager() {
    }

    public Manager(String name, Integer id, Double salary, Double bonus) {
        this.name = name;
        this.id = id;
        this.salary = salary;
        this.bonus = bonus;
    }

    /**
     * 获取
     *
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     *
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     *
     * @return id
     */
    public Integer getId() {
        return id;
    }

    /**
     * 设置
     *
     * @param id
     */
    public void setId(Integer id) {
        this.id = id;
    }

    /**
     * 获取
     *
     * @return salary
     */
    public Double getSalary() {
        return salary;
    }

    /**
     * 设置
     *
     * @param salary
     */
    public void setSalary(Double salary) {
        this.salary = salary;
    }

    /**
     * 获取
     *
     * @return bonus
     */
    public Double getBonus() {
        return bonus;
    }

    /**
     * 设置
     *
     * @param bonus
     */
    public void setBonus(Double bonus) {
        this.bonus = bonus;
    }

    public String toString() {
        return "Manager{name = " + name + ", id = " + id + ", salary = " + salary + ", bonus = " + bonus + "}";
    }


    public static void main(String[] args) {
        Manager manager = new Manager("张三", 1, 20000.0, 1000.0);
        manager.work();
    }
}

```



```java
package com.itheima.homework;

public class Coder {

    private String name;

    private Integer id;

    private Double salary;

    public void work() {
        System.out.println("工号为" + this.id + "基本工资为" + this.salary + "的程序员" + this.name + "正在努力的写着代码......");
    }

    public Coder() {
    }

    public Coder(String name, Integer id, Double salary) {
        this.name = name;
        this.id = id;
        this.salary = salary;
    }

    /**
     * 获取
     *
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     *
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     *
     * @return id
     */
    public Integer getId() {
        return id;
    }

    /**
     * 设置
     *
     * @param id
     */
    public void setId(Integer id) {
        this.id = id;
    }

    /**
     * 获取
     *
     * @return salary
     */
    public Double getSalary() {
        return salary;
    }

    /**
     * 设置
     *
     * @param salary
     */
    public void setSalary(Double salary) {
        this.salary = salary;
    }

    public String toString() {
        return "Coder{name = " + name + ", id = " + id + ", salary = " + salary + "}";
    }


    public static void main(String[] args) {
        Coder coder = new Coder("张三", 1, 20000.0);
        coder.work();
    }
}

```

