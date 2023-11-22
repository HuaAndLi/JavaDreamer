# 每日作业 - JavaSE第4天

## 选择题

### 题目1(单选):

##### 		下列代码的运行结果是( A )

```Java
public class test {
        public static void main(String[] args) {
            int sum = 0;
            int i=0;
            while (i<=5){
                if(i % 2 != 0){
                    sum += i;
                }
                i++;
            }
            System.out.println("sum = " + sum);
        }
}
```

#### 选项:

​	A. sum = 9 

​	B. sum = 6 

​	C. sum = 15 

​	D. sum = 0 

-----

### 题目2(单选): 

##### 		以下代码片段执行后,控制台的输出结果为( A ) 

```Java
public static void main(String[] args) {
    int sum=0;
    int i=1;
    while(i<3){
        sum+=i;
        i++;
    }
    System.out.print("sum="+sum);
}
```

#### 选项:

​	A. sum=3 

​	B. sum=0  

​	C. sum=6  

​	D. sum=1 

-----

### 题目3(单选):

##### 		下列代码的运行结果是( B )

```Java
public class Test {
    public static void main(String[] args) {
        int sum = 0;
        for(int i = 0; i < 10; i++){
           if (i % 3 != 0){
               sum += i;
           }
        }
        System.out.println("sum = " + sum);
    }
}
```

#### 选项:

​	A. sum = 45 

​	B. sum = 27 

​	C. sum = 18 

​	D. sum = 55 

-----

### 题目4(单选): 

##### 		阅读代码,下面那些代码片段能够求1~10(包含1也包含10)之间偶数的和( A ) 

#### 选项:

A.

```Java
int sum=0;
for(int i=1;i<=10;i++){
    if(i%2==0){
        sum+=i;
    }
}
```

B.

```Java
int sum=0;
for(int i=1;i<10;i+=2){
    sum+=i;
}
```

C.

```Java
int sum=0;
for(int i=1;i<10;i++){
    if(i%2!=0){
        sum+=i;
    }
}
```

D.

```Java
int sum=0;
for(int i=0;i<=10;i+=2){
    sum+=i;
}
```

-----

### 题目5(单选):

##### 		关于for循环语句说法错误的是(<font size=3 color=red>**A**</font>)

```Java
for (初始化语句; 循环判断表达式; 步进语句) {
    ①int a = 10;
    ②循环体;
}
```

#### 选项:

​	A. 因为初始化语句在循环中只执行一次,所以循环过程中, 无法使用初始化语句中定义的变量.

​	B. 循环判断表达式的执行次数,会比循环体的执行次数多一次. 

​	C. ①处定义的变量a,每一次进入循环,都会重新定义一个新的变量. 

​	D. 循环体是否执行,需要根据[循环判断表达式]返回的true或false而定. 

-----

### 题目6(单选): 

##### 		下列代码的运行结果是( D ) 

```Java
public static void main(String [] args){
	int i = 1;
	while(i == 10){
		++i;
		System.out.println("执行循环啦");
	}
}
```

#### 选项:

​	A.语法错误. 

​	B.打印9次执行循环啦. 

​	C.打印10次执行循环啦. 

​	D.没有输出结果. 

-----

### 题目7(单选) :

##### 		下列代码的运行结果是( A )

```Java
public static void main(String[] args) {
    int count = 0;
    int i = 2;
    while( i < 7){
        if (i % 2 == 1){
            count++;
        }
            
        i++;
    }
   	System.out.println(count);
}
```

#### 选项:

​	A.2

​	B.3

​	C.4

​	D.5

-----

### 题目8(单选): 

##### 		下面有关do...while循环的执行流程,那些描述是正确的( B ) 

#### 选项:

​	A.do...while循环在循环条件成立的情况下,循环语句体才能被执行. 

​	B.do...while循环的循环条件即使不成立,循环语句体也能被执行1次. 

​	C.do...while循环的循环语句体只能被执行一次.

​	D.do...while是先判断循环条件是否成立,再执行循环语句体.

------



## 代码题

### 题目9:

##### 		在中国历法中有十二生肖年份,2019年是己亥猪年,请在控制台输出从1949年(包含)到2019年(包含)中所有是猪年的年份。

##### 参考步骤:

1. 定义for循环,1949到2019的年份是循环次数.

2. 对每个年份逐个判断,如果年份和2019的差值是12的倍数,说明这年是猪年.

3. 打印符合条件的年份.


##### 参考答案:

```Java
public class Demo1 {
    public static void main(String[] args) {
        //1.循环开始是1949 结束是2019
        for (int i = 1949; i <= 2019; i++) {
            //2.如果年份和2019年的差值是12的倍数 则说明是猪年
            if( (2019 - i) % 12 == 0 ){
                //3.打印符合条件的年份
                System.out.println(i);
            }
        }
    }
}
```

------



### 题目10:

##### 	中国使用的公历有闰年的说法,闰年的规则是:四年一闰,百年不闰,四百年再闰。(年份能够被4整除但不能被100整除算是闰年,年份能被400整除也是闰年).请打印出1988年到2019年的所有闰年年份。

##### 参考步骤:

1. 定义for循环,循环变量开始是1988,结束是2019.

2. 在循环中对年份进行判断,判读条件为:可以被4整除,并且不可以被100整除,或者可以被400整除.

3. 如果符合条件,输出该年份.


##### 参考答案:

```Java
public class Demo6 {
    public static void main(String[] args) {
        //1. 定义对年份的循环
        for (int year = 1988; year <= 2019; year++) {
            //2. 判断当年是否符合闰年条件
            if((year%4 == 0 && year%100 != 0) || year%400 == 0){
                System.out.println(year + "是闰年");
            }
        }
    }
}
```

