# 选择题

### 题目1(多选): 

下面关于方法的概述描述，正确的是（ABD ） 

选项 : 

A:  方法定义的先后顺序无所谓 

B:  方法的定义不能产生嵌套包含关系。 

C:  方法可以让程序的执行效率更高 

D:  方法定义好了之后，不会执行的，如果要想执行，一定要进行方法的调用 



------

### 题目2(多选): 

以下选项中，关于方法定义的参数或返回值描述正确的是（ABD ） 

选项 : 

A:  方法的参数可以有，可以没有，也可以有多个 

B:  方法的参数就是定义一些变量，当方法被调用的时候，用来接收数据使用的 

C:  一个方法执行完成之后可以有一个返回值 ,也可以有多个返回值

D:  方法的返回值是方法执行完成之后得到的结果 



------

### 题目3(单选): 

代码如下：

```java
public static void main(String[] args){
   ________________________________
}

public static void method(){
    System.out.println("我是程序员");
}
```

​	运行结果是：

​	我是程序员

​	横线处应该填写的正确代码是（C ）

选项 : 

A:  method;

B:  void v = method();

C:  method();

D:  method("我是程序员");



------

### 题目4(单选): 

​	请观察以下代码，分别为第三行和第六行选出正确选项，保证可以在控制台上输出 

```java
public class Test08 {
    public static void main(String[] args){
	    _____①_____
    }

    public _____②_____ print() {	
        System.out.println("wo ai java");
    }
}
```

​	运行结果是：

​	wo ai java

​	横线处应该填写的正确代码是（B）

选项 : 

A:  ①  void v = print();		②  static void	

B:  ①  print();				②  static void    

C:  ①  int v = print();		②  static int	

D:  ①  print();			②  static	



------

### 题目5(单选): 

​	下列方法定义格式正确的是（B ） 

```java
A:
public static void method1(){
    public static void method2(){
    }
}

B:
public static void method1(){
}

C:
public static void method1(){
   return 10;
}

D:
public static boolean method1(int n){
    if(n < 10){
        return false;
    }else if(n > 10){
		return true;
	}
}
```

选项 : 

A:  选择A

B:  选择B

C:  选择C

D:  选择D



------

### 题目6(单选): 

观察以下代码，请选出方法调用过程的正确顺序（D）

```java
public static void main(String[] args) {
    System.out.println("开始执行");	   //1
    int a = print(10);                //2
    System.out.println(a);		     //3
}
public static int print(int n){    	 //4
    n += 10;                         //5
    return n;          			    //6
}
```

选项 : 

A:  1，2，3，4，5，6  

B:  1，2，4，6，5，3 

C:  1，4，5，6，2，3 

D:  1，2，4，5，6，3  



------

### 题目7(多选): 

​	以下选项中，关于方法的调用过程描述正确的是 (ACD) 

```java
public class Demo{
  public static void main(String[] args) {
     int a = 10;
     int b = 20;
     int sum = getSum(a,b);
     System.out.println(sum);
     isEquals(a, b);
  }

  public static int getSum(int a,int b){
     int sum = a + b;
     return sum;
  }
  
  public static void isEquals(int a,int b){
    boolean c = a == b;
    System.out.println(c);
  }
}
```

选项 : 

A:  由java虚拟机调用main方法，main方法先执行 

B:  在main方法执行中，会定义a和b变量，并分别赋值10和20，然后先调用isEquals方法，再调用getSum方		 		法并输出结果 

C:  调用getSum方法时，要先传入两个整数，否则编译失败。然后执行getSum方法内的代码，执行完成之后，将结果返回赋值给int类型的变量sum 

D:  调用isEquals方法时，要先传入两个整数，否则编译失败。然后执行isEquals方法内的代码，执行完成之后，没有结果返回 

### 题目8(单选): 

​	以下选项中，不属于方法重载的是（ B） 

```java
A:
public class Demo{
  public int getSum(int a,byte b){
    return a + b;
  }
  
  public int getSum(int a,int b){
    return a + b;
  }
}

B：
public class Demo{ // 参数名无关紧要，类型都是一样的
  public int getSum(int b,int a){
    return a + b;
  }
  
  public void getSum(int a,int b){
    System.out.println(a + b);
  }
}

C:
public class Demo{
  public long getSum(long a,int b){
    return a + b;
  }
  
  public long getSum(int a,long b){
    return a + b;
  }
}

D:
public class Demo{
  public void getSum(int a,int b){
    System.out.println(a + b);
  }
  
  public int getSum(int a,int b,int c){
    return a + b + c;
  }
}
```



------

### 题目9(单选): 

​	观察下面代码，最终在控制台显示 33 正确的方法调用格式是（C ） 

```java
public static void main(String[] args){
    //此处需要调用下面的某个方法，在控制台当中显示33
}

public static void printData(int a,int b){
    System.out.println(11); 
}

public static void printData(int a){
    System.out.println(22); 
}

public static void printData(boolean b){
    System.out.println(33); 
}

public static void printData(){
    System.out.println(44); 
}
```

选项 : 

A:  printData(10,20);

B:  printData(333);

C:  printData(true)

D:  printData();



# 编程题

方法

## 题目1:

定义一个方法，该方法能够找出三个整数中的最大值并返回。在主方法中调用方法测试执行。

### 训练提示

1. 根据题意，方法中需要使用三个整数，所以方法参数应该是三个整数类型。
2. 方法需要有返回值，返回值的类型也是整数类型。

### 操作步骤

1. 定义方法getMax()，方法的参数是三个int类型变量a,b,c，方法的返回值是int类型。
2. 在方法中使用多分支if...else...判断出最大值并返回。
3. 在主方法中调用getMax()方法并接受返回值。
4. 在主方法中打印结果。

### 参考代码

```java
public class Test1 {
    public static void main(String[] args) {
        //调用方法传入参数
        int max = getMax(33, 44, 11);
        //打印最大值
        System.out.println("最大值是" + max);


    }
    //定义获取最大值的方法
    public static int getMax(int a ,int b ,int c){
        //判断出最大值并返回
        int tempMax = a > b ? a : b;
        int max = tempMax > c ? tempMax : c;
        return max;
    }
}
```



## 题目2:

请定义一个方法，该方法可以实现对int类型的数组进行遍历，在控制台打印所有元素。实现方法后，请在主方法中调用方法，查看结果。例如，数组为{11, 22, 33}，打印格式为：[11, 22, 33] 

### 训练提示

1、首先明确方法的返回值和参数列表，该方法只需要在控制台输出，f返回值类型为void.要实现打印数组元素的功能，需要方法的调用者把想打印的数组传递过来，所以参数列表是int[] arr

2、方法实现之后，不调用的话会执行吗？该怎样调用？

### 操作步骤

1、定义方法，返回值类型为void，参数列表为int[] arr

2、在方法中，遍历数组，判断是否是最后一个元素，并且根据不同的情况输出不同的格式。

3、在主方法中定义一个数组，调用方法，将数组作为参数传递，查看运行结果。

### 参考代码

```java
public class Test2 {
    public static void main(String[] args) {
        int[] arr = {11, 22, 33};
        printArr(arr);
    }

    public static void printArr(int[] arr) {
        // [11, 22, 33] 先打印左边[，注意不要回车
        System.out.print("[");
        // 遍历数组
        for (int i = 0; i < arr.length; i++) {
            // 判断是否是最后一个元素
            if (i == arr.length - 1) {
                System.out.print(arr[i]);
            } else {
                // 中间的元素，要多打印一个逗号和空格
                System.out.print(arr[i] + ", ");
            }
        }
        // 循环结束，再打印一个右边的]，最后的打印加换行
        System.out.println("]");
    }
}
```

