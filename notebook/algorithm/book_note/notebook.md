## 简介 

《算法图解》笔记

# 第一章 算法简介

## 代码

### 二分查找

```java
    /**
     * 二分查找
     *
     * @param arr  需要查找的数组
     * @param item 查找的元素
     * @return 返回元素下标
     */
    Integer binary_search(int[] arr, int item) {
        int low = 0;
        int high = arr.length - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] == item) {
                return mid;
            } else if (arr[mid] > item) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return null;
    }

    @Test
    void testMain() {
        int[] my_arr = new int[]{1, 3, 5, 7, 9};

        System.out.println(binary_search(my_arr, 3));//1
        System.out.println(binary_search(my_arr, -1));//null
    }
```



## 课后作业

**1.1 假设有一个包含128个名字的有序列表，你要使用二分查找在其中查找一个名字，请 问最多需要几步才能找到？** 

log(128) = 7

**1.2 上面列表的长度翻倍后，最多需要几步？**

8

**1.3 在电话簿中根据名字查找电话号码。 使用大O表示法给出下述各种情形的运行时间。**

根据字母姓式二分查找所用时间为:O(log n)

**1.4 在电话簿中根据电话号码找人。（提示：你必须查找整个电话簿。）** 

简单查找，所用时间为:O(n)

**1.5 阅读电话簿中每个人的电话号码。** 

简单查找，所用时间为：O(n)

**1.6 阅读电话簿中姓名以A打头的人的电话号码。这个问题比较棘手，它涉及第4章的概 念。答案可能让你感到惊讶！**

简单查找，所用时间为：O(n)





# 第二章 选择排序

## 代码

### 选择排序

这里书上写的过于复杂，自己实现。

```java
    /**
     * 选择排序
     * 因为引用传递，所以不需要返回值。
     * 思路：遍历数组，每次选择最小值，换到前面。
     *
     * @param arr
     */
    void selectionSort(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            int minIndex = i;//最小值下标，初试为当前值
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }
            int temp = arr[i];//交换位置。
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }

    }

    @Test
    void testMain() {
        int[] my_arr = new int[]{5, 3, 6, 2, 10};
        selectionSort(my_arr);
        Arrays.stream(my_arr).forEach((e) -> System.out.print(e));//235610
    }
```



## 课后作业

**2.1 假设你要编写一个记账的应用程序。“1.买杂货2.看电影3.会费” 你每天都将所有的支出记录下来，并在月底统计支出，算算当月花了多少钱。因此， 你执行的插入操作很多，但读取操作很少。该使用数组还是链表呢？**

链表，插入O(1),读取O（n）

**2.2 假设你要为饭店创建一个接受顾客点菜单的应用程序。这个应用程序存储一系列点菜 单。服务员添加点菜单，而厨师取出点菜单并制作菜肴。这是一个点菜单队列：服务 员在队尾添加点菜单，厨师取出队列开头的点菜单并制作菜肴。 你使用数组还是链表来实现这个队列呢？（提示：链表擅长插入和删除，而数组擅长 随机访问。在这个应用程序中，你要执行的是哪些操作呢？）** 

<img src="./img/2023-11-19_10-48-16.png" style="zoom:33%;" />

使用链表，因为不需要随机访问，只有添加和删除操作。

**2.3 我们来做一个思考实验。假设Facebook记录一系列用户名，每当有用户试图登录 Facebook时，都查找其用户名，如果找到就允许用户登录。由于经常有用户登录 Facebook，因此需要执行大量的用户名查找操作。假设Facebook使用二分查找算法， 而这种算法要求能够随机访问——立即获取中间的用户名。考虑到这一点，应使用数 组还是链表来存储用户名呢？** 

使用数组，目前没有添加操作，并且二分查找必须要随机访问。

**2.4 经常有用户在Facebook注册。假设你已决定使用数组来存储用户名，在插入方面数组 有何缺点呢？具体地说，在数组中添加新用户将出现什么情况？** 

缺点，由于要支持二分查找，所以用户存储必须有序，所以添加新用户，可能需要大量移动元素，时间复杂度：O(n)。并且若内存中位置不足，需要全部移动位置。

**2.5 实际上，Facebook存储用户信息时使用的既不是数组也不是链表。假设Facebook使用 的是一种混合数据：链表数组。这个数组包含26个元素，每个元素都指向一个链表。 例如，该数组的第一个元素指向的链表包含所有以A打头的用户名，第二个元素指向的 链表包含所有以B打头的用户名，以此类推。 假设Adit B在Facebook注册，而你需要将其加入前述数据结构中。因此，你访问数组的 第一个元素，再访问该元素指向的链表，并将Adit B添加到这个链表末尾。现在假设你要查找Zakhir H。因此你访问第26个元素，再在它指向的链表（该链表包含所有以z打 头的用户名）中查找Zakhir H。 请问，相比于数组和链表，这种混合数据结构的查找和插入速度更慢还是更快？你不 必给出大O运行时间，只需指出这种新数据结构的查找和插入速度更快还是更慢。**

<img src="./img/2023-11-19_10-50-18.png" style="zoom:33%;" />

这种数据结构，相比于数组，插入更快，查找稍慢。相比于链表查找较快，插入较慢。

# 第三章 递归

## 代码

**递归倒计时**

```java
    /**
     * 递归倒计时
     *
     * @param time 开始的倒计时
     *             输出：time time-1 ... time-n;
     */
    static void countDown(int time) {
        if (time < 1) {
            return;
        } else {
            System.out.println(time);
            countDown(time - 1);
        }
    }

    public static void main(String[] args) {
        countDown(5);// 5 4 3 2 1
    }

```

**递归阶乘**

```java
    /**
     * 递归阶乘
     *
     * @param n
     * @return n!
     */
    static int facMul(int n) {
        if (n <= 1) {
            return 1;
        } else {
            return n * facMul(n - 1);
        }
    }
    public static void main(String[] args) {
        System.out.println(facMul(4));//24
    }

```



## 课后作业

**3.1 根据下面的调用栈，你可获得哪些信息？**

<img src="./img/20231120104811.png" style="zoom:50%;" />

greet方法先被调用，name参数出入maggle

great方法中调用了greet2方法，name参数传入maggle

此时greet未完成

正在调用greet2，若greet2中无其他调用方法，greet2调用玩，返回greet方法继续执行。

**3.2 假设你编写了一个递归函数，但不小心导致它没完没了地运行。正如你看到的，对于 每次函数调用，计算机都将为其在栈中分配内存。递归函数没完没了地运行时，将给 栈带来什么影响？**

内存溢出。





