## 选择题

### 题目1(单选):

**下面哪个可以正确的获取数组a的第三个元素( D )**

#### 选项 :   

​	A、a(3)         
​	B、a[3]    
​	C、a(2)         
​	D、a[2]

-----

### 题目2(单选):

**下面哪个选项可以正确的创建出字符数组( C )**

#### 选项 :   

​	A. char[] str="hello";    

​	B. char[5] str="hello";  

​	C. char[] str={'h','e','l','l','o'};       

​	D. char[] str={"hello"}; 

----------

### 题目3(单选):

**我们使用关键字new创建出来的数组会保存到内存的哪个位置( C )**

#### 选项 :   

​	A、栈
​	B、队列
​	C、堆
​	D、CPU

---

### 题目4(单选):

关于数组默认值，错误的是（ B ）

#### 选项 :   

​	A、double --0.0

​	B、boolean--true

​	C、String -- null

​	D、int--0

----

### 题目5(单选):

下面代码中，如果想要在控制台显示 6 ，那么下列横线处的正确书写内容应该是（ C）

```java
public static void main(String[] args){
    int[] arr = { 3,6,9,2,5,8 };
    System.out.println(____________);
}
```

#### 选项 :   

​	A: arr[6]

​	B: arr[2]

​	C: arr[1]

​	D: arr[0]

---

### 题目6(单选):

下列代码的运行结果是（ D ）

```java
public static void main(String[] args) {
    int arr[] = {1, 3, 5, 7, 9};
    System.out.println("结果是："+arr[1]);
    System.out.println("结果是："+arr[arr.length-1]);
}
```

#### 选项 :   

A:     结果是：1
	结果是：9 	
B:     结果是：1
	结果是：7 
C:     结果是：3
	结果是：7 
D:    结果是：3
	结果是：9  

---

### 题目7(单选):

下面代码执行之后，控制台显示的结果是（ D ）

```java
public static void main(String[] args){
    int[] arr = new int[5];
    System.out.println(arr[5]);
}
```

#### 选项 :  

​	A:  0

​	B:  控制台没有任何显示

​	C:  NullPointerException

​	D:  ArrayIndexOutOfBoundsException

---

### 题目8(单选):

下列哪些代码能够正常执行（ D ）

#### 选项 : 

```java
A：

public class Demo{
    public static void main(String[] args){
        int[] arr = {1,2,3,4};
        int i = arr[4];
    }
}
B：

public class Demo{
    public static void main(String[] args){
        int[] arr = null;
        int i = arr[0];
    }
}
C：

public class Demo{
    public static void main(String[] args){
        int[] arr = {1,2,3,4};
        arr = 1;
    }
}
D：

public class Demo{
    public static void main(String[] args){
        int[] arr = new int[5];
        int i = arr[2];
    }
}  
```

---

### 题目9(单选):

下面是遍历输出数组每个元素的代码，请在代码区域当中（1）和（2）位置，补上正确的代码（ C）

```java
public static void main(String[] args){
    int[] arr = { 2,7,1,6,3 };
    for( int i = 0 ; ____(1)____ ; i++ ){
        System.out.println(____(2)____);`
    }
}
```

#### 选项 : 

A:

(1)i<arr.length-1
(2)arr[i]

B:

(1)i<=arr.length-1
(2)arr 

C:

(1)i<=arr.length-1
(2)arr[i] 

D:

(1)i<arr.length-1
(2)arr

---

### 题目10(单选):

下列代码用于获取数组中元素的最大值，横线处应该填写的正确代码是（ C ）

```java
public static void main(String[] args){
    int[] arr = { -9, -5, -2, -7 };
    ________①_______
    for(int i=1; i<arr.length; i++){
        if(_____②_____){
           _____③_____
        }
    }
    System.out.println("最大值是:" + max);
}
```

#### 选项 : 

A．

```java
①int max = 0;	
②arr[i] < max	
③arr[i] = max; 
```

B．

```java
①int max = 0;	
②arr[i] > max	
③max = arr[i]; 	
```

C．

```java
①int max = arr[0];	
②arr[i] > max	
③max = arr[i]; 	
```

D．

```java
①int max = arr[i];	
②arr[i] > max	
③max = arr[i]; 	
```

---

### 题目11(单选):

下列代码的运行结果是（ B ）

```java
public static void main(String[] args) {
    int[] arr = { 9, 5, 2, 7 };
    		

    for(int i=0;i<arr.length;i++){
        if( i % 2 != 0){
            arr[i]+=10;
        }
    }
    for (int i = 0; i < arr.length; i++) {
        System.out.print(arr[i]+" ");
    }
}
```

#### 选项 : 

​	A:  9  5  2  7 

​	B:  9  15  2  17 

​	C:  9  5  12  7 

​	D:  19  15  12  17 



## 编程题

数组

### 题目1（加强训练）

* 需求：定义一个长度为5的一维数组，给每个元素赋值. (要求数组中每个元素的值是20-80的随机数)

  遍历数组打印每个元素的值

**控制台输出效果:**

> 本题打印结果具有随机性

```java
随机数为:
72
52
65
51
78
```

#### 训练目标

1. 能够熟练使用数组动态初始化
2. 能够熟练掌握数组的遍历

#### 训练提示

* 随机数的 nextInt() 方法，( ) 里面无论写什么，都有0的可能性，题目要求最小的随机数是20，就应该在结果上加20.

#### 操作步骤

1. 准备Random
2. 动态初始化长度为5的一维数组
3. 遍历数组, 在遍历的过程中产生随机数并存入数组
4. 遍历打印数组

#### 参考答案

```java
public class HomeWork1 {
    /*
        需求：定义一个长度为5的一维数组，给每个元素赋值. (要求数组中每个元素的值是20-80的随机数)
            遍历数组打印每个元素的值

        分析:
            1. 准备Random
            2. 动态初始化长度为5的一维数组
            3. 遍历数组, 在遍历的过程中产生随机数并存入数组
            4. 遍历打印数组
     */
    public static void main(String[] args) {
        // 1. 准备Random
        Random r = new Random();
        // 2. 动态初始化长度为5的一维数组
        int[] arr = new int[5];
        // 3. 遍历数组, 在遍历的过程中产生随机数并存入数组
        for (int i = 0; i < arr.length; i++) {
            int randomNum = r.nextInt(61) + 20;
            arr[i] = randomNum;
        }
        System.out.println("随机数为:");
        // 4. 遍历打印数组
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}
```



### 题目2（加强训练）

* 需求：键盘录入一个整数作为数组的长度，随后再次键盘录入数据并将数组存满
  * 从数组中找出最小值，并将最小值打印在控制台



#### 训练目标

* 能够使用Scanner填充数组
* 能够在遍历数组过程中，加入 if 条件筛选

#### 训练提示

* 建议对数组遍历两次，第一次只做数据填充，第二次只找最大值

#### 操作步骤

       1. 准备Scanner
       2. 键盘录入一个整数, 根据这个整数动态初始化数组长度
       3. 遍历数组, 在遍历的过程中录入数据, 并存入数组
       4. 求最小值
       5. 打印最小值

#### 参考答案

```java
public class HomeWork2 {
    /*
        需求：键盘录入一个整数作为数组的长度，随后再次键盘录入数据并将数组存满
            从数组中找出最小值，并将最小值打印在控制台

     */
    public static void main(String[] args) {
        //1. 准备Scanner
        Scanner sc = new Scanner(System.in);
        //2. 键盘录入一个整数, 根据这个整数动态初始化数组长度
        System.out.println("请输入数组长度:");
        int length = sc.nextInt();

        int[] arr = new int[length];
        //3. 遍历数组, 在遍历的过程中录入数据, 并存入数组
        System.out.println("请输入元素:");
        for (int i = 0; i < arr.length; i++) {
            arr[i] = sc.nextInt();
        }

        //4. 求最小值
        int min = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] < min) {
                min = arr[i];
            }
        }
        //5. 打印最小值
        System.out.println("最小值为:" + min);
    }
}
```





