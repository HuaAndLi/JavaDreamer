# 简介

此文件为leetcode动态规划专栏刷题笔记，难度从简单->中等->困难。

网址：[动态规划知识点题库 - 力扣（LeetCode）](https://leetcode.cn/tag/dynamic-programming/problemset/?difficulty=Easy&premiumOnly=false)



# 简单

## [70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/)

### 问题

假设你正在爬楼梯。需要 `n` 阶你才能到达楼顶。

每次你可以爬 `1` 或 `2` 个台阶。你有多少种不同的方法可以爬到楼顶呢？

 

**示例 1：**

```
输入：n = 2
输出：2
解释：有两种方法可以爬到楼顶。
1. 1 阶 + 1 阶
2. 2 阶
```

**示例 2：**

```
输入：n = 3
输出：3
解释：有三种方法可以爬到楼顶。
1. 1 阶 + 1 阶 + 1 阶
2. 1 阶 + 2 阶
3. 2 阶 + 1 阶
```

 

**提示：**

- `1 <= n <= 45`

### 答案

**思路：**每次只能走一步或者2步。

- 上1阶  只能按照走一步的方式 ，1种
- 上2阶  可以在2-1阶往上一步，所以是1种；可以在2-2阶直接上去，1种；1+1等于2种。
- 上3阶 可以在3-1阶往上一步，所以是2种；可以在3-2阶往上走2步，所以是1种；1+2等于3种。
- 上4阶 可以在4-1阶往上一步，所以是3种，可以在4-2阶往上走2步，所以是2种；2+3等于5总。

总结规律，1阶为1种，2阶为2种，后面每个都是前面2阶的数量相加。

**代码实现：**

```java
public static int climbStairs(int n) {
        if (n <= 1) { //如果上1阶默认为1种
            return 1;
        }
        if (n == 2) {//如果上2阶为2种。
            return 2;
        }
        int before1 = 1;//-2阶
        int before2 = 2;//-1阶
        int sum = 0;//当前阶种
        for (int i = 2; i < n; i++) {
            sum = before1 + before2;//算一下当前台阶种数
            before1 = before2;//往上走
            before2 = sum;//往上走
        }
        return sum;
    }
```



## [118. 杨辉三角](https://leetcode.cn/problems/pascals-triangle/)

### 问题

给定一个非负整数 *`numRows`，*生成「杨辉三角」的前 *`numRows`* 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。

![img](https://pic.leetcode-cn.com/1626927345-DZmfxB-PascalTriangleAnimated2.gif)

 

**示例 1:**

```
输入: numRows = 5
输出: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

**示例 2:**

```
输入: numRows = 1
输出: [[1]]
```

 

**提示:**

- `1 <= numRows <= 30`

### 答案

**思路**

前面 numRows =1 ，2 固定返回；

后 numRows>2 时，获取（numRows-1）的list，遍历相加邻近两个数。不要忘记头和尾要添加1。

**代码实现**

```java
    public static List<List<Integer>> generate(int numRows) {
        List<List<Integer>> all = new ArrayList<>();//总list，用于返回

        List<Integer> item = new ArrayList<>();//每项的list
        Collections.addAll(item, 1);
        all.add(item);
        if (numRows <= 1) {//小于等一的情况，默认返回[[1]]
            return all;
        }
        item = new ArrayList<>();
        Collections.addAll(item, 1, 1);
        all.add(item);
        if (numRows == 2) {//等于2的情况，返回[[1],[1,1]]
            return all;
        }
        for (int i = 2; i < numRows; i++) {//循环大于2的情况
            item = new ArrayList<>();//新建item
            item.add(1);//最前面的1
            List<Integer> beforeItem = all.get(i - 1);//获取前面一个list
            for (int i1 = 0; i1 < beforeItem.size() - 1; i1++) {//遍历前面一个list
                item.add(beforeItem.get(i1) + beforeItem.get(i1 + 1));//两两相加添加。
            }
            item.add(1);//最后面的1
            all.add(item);//添加总list
        }
        return all;
    }
```



##  [119. 杨辉三角 II](https://leetcode.cn/problems/pascals-triangle-ii/)

### 问题

给定一个非负索引 `rowIndex`，返回「杨辉三角」的第 `rowIndex` 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。

![img](https://pic.leetcode-cn.com/1626927345-DZmfxB-PascalTriangleAnimated2.gif)

 

**示例 1:**

```
输入: rowIndex = 3
输出: [1,3,3,1]
```

**示例 2:**

```
输入: rowIndex = 0
输出: [1]
```

**示例 3:**

```
输入: rowIndex = 1
输出: [1,1]
```

 

**提示:**

- `0 <= rowIndex <= 33`

 

**进阶：**

你可以优化你的算法到 `*O*(*rowIndex*)` 空间复杂度吗？

### 答案

**思路**

可以在上一题的基础上进行修改即可。每次使用一个临时变量记录新的item，最后赋值后垃圾回收机制会自动处理。

**代码实现**

```java
    public List<Integer> getRow(int rowIndex) {
        List<Integer> item = new ArrayList<>();//返回的list
        Collections.addAll(item, 1);
        if (rowIndex <= 0) {//<=0的情况，默认返回[1]
            return item;
        }
        item = new ArrayList<>();
        Collections.addAll(item, 1, 1);
        if (rowIndex == 1) {//等于1的情况，返回[1,1]
            return item;
        }
        for (int i = 1; i < rowIndex; i++) {//循环大于1的情况
            List<Integer> nowItem = new ArrayList<>();//当前要生成的list
            nowItem.add(1);//头添加1
            for (int i1 = 0; i1 < item.size() - 1; i1++) {//遍历前面一个list
                nowItem.add(item.get(i1) + item.get(i1 + 1));//两两相加添加。
            }
            nowItem.add(1);//最后面的1
            item = nowItem;//item指向新的newItem，不用担心之前的没有引用垃圾回收会处理。
        }
        return item;
    }
```



## [121. 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)

### 问题

给定一个数组 `prices` ，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i` 天的价格。

你只能选择 **某一天** 买入这只股票，并选择在 **未来的某一个不同的日子** 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 `0` 。

 

**示例 1：**

```
输入：[7,1,5,3,6,4]
输出：5
解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
```

**示例 2：**

```
输入：prices = [7,6,4,3,1]
输出：0
解释：在这种情况下, 没有交易完成, 所以最大利润为 0。
```

 

**提示：**

- `1 <= prices.length <= 105`
- `0 <= prices[i] <= 104`

### 答案

**思路**

不要把问题复杂化，从前往后遍历，每次记录最低值，并且max（当前利润，之前的利润）。

**代码实现**

```java
public int maxProfit(int[] prices) {
        int profit = 0;//利润最低为0
        int minNum = Integer.MAX_VALUE;//记录最小值
        for (int price : prices) {
            minNum = Math.min(price, minNum);//更新最小值
            profit = Math.max(profit, price - minNum);//更新最大利润
        }
        return profit;
    }
```



## [338. 比特位计数](https://leetcode.cn/problems/counting-bits/)

### 问题

给你一个整数 `n` ，对于 `0 <= i <= n` 中的每个 `i` ，计算其二进制表示中 **`1` 的个数** ，返回一个长度为 `n + 1` 的数组 `ans` 作为答案。

 

**示例 1：**

```
输入：n = 2
输出：[0,1,1]
解释：
0 --> 0
1 --> 1
2 --> 10
```

**示例 2：**

```
输入：n = 5
输出：[0,1,1,2,1,2]
解释：
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
```

 

**提示：**

- `0 <= n <= 105`

 

**进阶：**

- 很容易就能实现时间复杂度为 `O(n log n)` 的解决方案，你可以在线性时间复杂度 `O(n)` 内用一趟扫描解决此问题吗？
- 你能不使用任何内置函数解决此问题吗？（如，C++ 中的 `__builtin_popcount` ）



### 答案

**思路**

这题解法两种，一直接调用Java自带的Integer.bitCount()。

二使用动态规划思想。

**代码实现**

直接调用Integer.bitCount()

```java
class Solution {
    public int[] countBits(int n) {
        int[] re_arr = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            re_arr[i] = Integer.bitCount(i);
        }

        return re_arr;
    }
}
```

自己实现bitCount()方法

```java
public static int myBitCount(int x) {
        int count = 0;
        while (x > 0) {
            x &= (x - 1);//去掉一个最低位
            count++;
        }
        return count;
    }
```

动态规划

```java
public static int[] countBits(int n) {
        int[] re_arr = new int[n + 1];
        re_arr[0] = 0;//初始一个个值，可以不写，默认为0，防止意外
        int maxBit = 0;//最大的2^n；
        for (int i = 1; i <= n; i++) {
            if ((i & (i - 1)) == 0) {
                maxBit = i;//记录
            }
            re_arr[i] = re_arr[i - maxBit] + 1;//减去当前最大bit的个数+1个最大bit
        }

        return re_arr;
    }
```



## [392. 判断子序列](https://leetcode.cn/problems/is-subsequence/)

### 问题

给定字符串 **s** 和 **t** ，判断 **s** 是否为 **t** 的子序列。

字符串的一个子序列是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，`"ace"`是`"abcde"`的一个子序列，而`"aec"`不是）。

**进阶：**

如果有大量输入的 S，称作 S1, S2, ... , Sk 其中 k >= 10亿，你需要依次检查它们是否为 T 的子序列。在这种情况下，你会怎样改变代码？

**致谢：**

特别感谢 [@pbrother ](https://leetcode.com/pbrother/)添加此问题并且创建所有测试用例。

 

**示例 1：**

```
输入：s = "abc", t = "ahbgdc"
输出：true
```

**示例 2：**

```
输入：s = "axc", t = "ahbgdc"
输出：false
```

 

**提示：**

- `0 <= s.length <= 100`
- `0 <= t.length <= 10^4`
- 两个字符串都只由小写字符组成。



### 答案

**思路**

我没有太看出来是动态规划，双指针遇到相同的往后移动，最后如果s超过末尾则true，反之false

**代码实现**

双指针

```java
public boolean isSubsequence(String s, String t) {
        int s_index = 0, t_index = 0, s_n = s.length(), t_n = t.length();
        while (s_index < s_n && t_index < t_n) {//都要没有到头
            if (s.charAt(s_index) == t.charAt(t_index)) {//如果相同子串就后移
                s_index++;
            }
            t_index++;//每次都要后移
        }

        return s_index == s_n;//如果字串到头就符合
    }
```

个人感觉动态规划也不怎么简单，有兴趣可以去研究一下。



## [509. 斐波那契数](https://leetcode.cn/problems/fibonacci-number/)

### 问题

**斐波那契数** （通常用 `F(n)` 表示）形成的序列称为 **斐波那契数列** 。该数列由 `0` 和 `1` 开始，后面的每一项数字都是前面两项数字的和。也就是：

```
F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
```

给定 `n` ，请计算 `F(n)` 。

 

**示例 1：**

```
输入：n = 2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1
```

**示例 2：**

```
输入：n = 3
输出：2
解释：F(3) = F(2) + F(1) = 1 + 1 = 2
```

**示例 3：**

```
输入：n = 4
输出：3
解释：F(4) = F(3) + F(2) = 2 + 1 = 3
```

 

**提示：**

- `0 <= n <= 30`

### 答案

**思路**

两个数记录前两个，后面加了之后，依次往前面两个换。

**代码实现**

```java
   public static int fib(int n) {
        if (n <= 0) {//<=0,默认为0
            return 0;
        }
        if (n == 1) {//==1，为1
            return 1;
        }
        int a = 0;
        int b = 1;
        for (int i = 1; i < n; i++) {
            int temp = a + b;//累计前两个
            a = b;//往前换值
            b = temp;
        }
        return b;
    }
```



## [746. 使用最小花费爬楼梯](https://leetcode.cn/problems/min-cost-climbing-stairs/)

### 问题

给你一个整数数组 `cost` ，其中 `cost[i]` 是从楼梯第 `i` 个台阶向上爬需要支付的费用。一旦你支付此费用，即可选择向上爬一个或者两个台阶。

你可以选择从下标为 `0` 或下标为 `1` 的台阶开始爬楼梯。

请你计算并返回达到楼梯顶部的最低花费。

 

**示例 1：**

```
输入：cost = [10,15,20]
输出：15
解释：你将从下标为 1 的台阶开始。
- 支付 15 ，向上爬两个台阶，到达楼梯顶部。
总花费为 15 。
```

**示例 2：**

```
输入：cost = [1,100,1,1,1,100,1,1,100,1]
输出：6
解释：你将从下标为 0 的台阶开始。
- 支付 1 ，向上爬两个台阶，到达下标为 2 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 4 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 6 的台阶。
- 支付 1 ，向上爬一个台阶，到达下标为 7 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 9 的台阶。
- 支付 1 ，向上爬一个台阶，到达楼梯顶部。
总花费为 6 。
```

 

**提示：**

- `2 <= cost.length <= 1000`
- `0 <= cost[i] <= 999`

### 答案

**思路**

首先，要爬上的台阶，要比cost数组长度多1个！动态规划，前两个台阶需要爬0次，

1阶   0

2阶  0

3阶  选择1阶或2阶往上，1阶已有的cost+1阶的cost；2阶已经有的cost+2阶的cost；比较选个小的。

4阶 选择2阶或3阶往上，2阶已有的cost+2阶的cost；3阶已经有的cost+3阶的cost；比较选个小的。

。。。。

n阶 = min(n-1阶已累计的cost+cost[n-1]，n-2阶已累计的cost+cost[n-2])

记住我们求的是n+1阶。

**代码实现**

```java
    public int minCostClimbingStairs(int[] cost) {
        if(cost.length<=1){//上前两阶不用爬
            return 0;
        }
        int a = 0;//上两阶为0
        int b = 0;

        for(int i = 2;i<=cost.length;i++){//这里判断条件是<= 因为要上n+1阶
            int temp = Math.min(a+cost[i-2],b+cost[i-1]);//选择最小的cost
            a = b;//替换前面的
            b = temp;
        }
        return b;
    }
```

 

## [1025. 除数博弈](https://leetcode.cn/problems/divisor-game/)

### 问题

爱丽丝和鲍勃一起玩游戏，他们轮流行动。爱丽丝先手开局。

最初，黑板上有一个数字 `n` 。在每个玩家的回合，玩家需要执行以下操作：

- 选出任一 `x`，满足 `0 < x < n` 且 `n % x == 0` 。
- 用 `n - x` 替换黑板上的数字 `n` 。

如果玩家无法执行这些操作，就会输掉游戏。

*只有在爱丽丝在游戏中取得胜利时才返回 `true` 。假设两个玩家都以最佳状态参与游戏。*

 



**示例 1：**

```
输入：n = 2
输出：true
解释：爱丽丝选择 1，鲍勃无法进行操作。
```

**示例 2：**

```
输入：n = 3
输出：false
解释：爱丽丝选择 1，鲍勃也选择 1，然后爱丽丝无法进行操作。
```

 

**提示：**

- `1 <= n <= 1000`

### 答案

**思路**

直接看代码注释

**代码实现**

```java
    public static boolean divisorGame(int n) {
        boolean[] arr = new boolean[n + 1];//从下标1开始用，多一个没事。
        //下标1默认是false,可以不用赋值。
        for (int i = 2; i < arr.length; i++) {//从2处理到n
            for (int x = i - 1; x > 0; x--) {//遍历0 < x < n中，满足n % x == 0的
                if (i % x == 0) {
                    arr[i] = !arr[i - x];//如果满足，说明我当前要比之前的多走一步，也就是做取反操作
                    if (arr[i] == true) {//因为我是先手，我肯定优先选择我能赢的情况。
                        break;
                    }
                }
            }
        }
        return arr[n];
    }
```

优化方法可以看官方。本人能力有限。



## [1137. 第 N 个泰波那契数](https://leetcode.cn/problems/n-th-tribonacci-number/)

### 问题

泰波那契序列 Tn 定义如下： 

T0 = 0, T1 = 1, T2 = 1, 且在 n >= 0 的条件下 Tn+3 = Tn + Tn+1 + Tn+2

给你整数 `n`，请返回第 n 个泰波那契数 Tn 的值。

 

**示例 1：**

```
输入：n = 4
输出：4
解释：
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
```

**示例 2：**

```
输入：n = 25
输出：1389537
```

 

**提示：**

- `0 <= n <= 37`
- 答案保证是一个 32 位整数，即 `answer <= 2^31 - 1`。

### 答案

**思路**

同理斐波那契数，只不过2个数换成了3个数。

**代码实现**

不解释

```java
    public int tribonacci(int n) {
        if (n == 0) {
            return 0;
        }
        if (n <= 2) {
            return 1;
        }
        int a = 0;
        int b = 1;
        int c = 1;

        for (int i = 2; i < n; i++) {
            int temp = a + b + c;
            a = b;
            b = c;
            c = temp;
        }

        return c;
    }
```



## [1646. 获取生成数组中的最大值](https://leetcode.cn/problems/get-maximum-in-generated-array/)

### 问题

给你一个整数 `n` 。按下述规则生成一个长度为 `n + 1` 的数组 `nums` ：

- `nums[0] = 0`
- `nums[1] = 1`
- 当 `2 <= 2 * i <= n` 时，`nums[2 * i] = nums[i]`
- 当 `2 <= 2 * i + 1 <= n` 时，`nums[2 * i + 1] = nums[i] + nums[i + 1]`

返回生成数组 `nums` 中的 **最大** 值。

 

**示例 1：**

```
输入：n = 7
输出：3
解释：根据规则：
  nums[0] = 0
  nums[1] = 1
  nums[(1 * 2) = 2] = nums[1] = 1
  nums[(1 * 2) + 1 = 3] = nums[1] + nums[2] = 1 + 1 = 2
  nums[(2 * 2) = 4] = nums[2] = 1
  nums[(2 * 2) + 1 = 5] = nums[2] + nums[3] = 1 + 2 = 3
  nums[(3 * 2) = 6] = nums[3] = 2
  nums[(3 * 2) + 1 = 7] = nums[3] + nums[4] = 2 + 1 = 3
因此，nums = [0,1,1,2,1,3,2,3]，最大值 3
```

**示例 2：**

```
输入：n = 2
输出：1
解释：根据规则，nums[0]、nums[1] 和 nums[2] 之中的最大值是 1
```

**示例 3：**

```
输入：n = 3
输出：2
解释：根据规则，nums[0]、nums[1]、nums[2] 和 nums[3] 之中的最大值是 2
```

 

**提示：**

- `0 <= n <= 100`

### 答案

**思路**

方法1：遍历一遍记录最大值。暴力。优化方法，将记录数组O（n）可以优化成O（1）。可以自己去尝试一下。

**代码实现**

```java
public int getMaximumGenerated(int n) {
        if (n == 0) {//特殊的返回条件
            return 0;
        }
        if (n == 1) {
            return 1;
        }
        int[] nums = new int[n + 1];
        nums[0] = 0;//初始化前两个
        nums[1] = 1;
        int max = 1;//当前最大的值
        for (int i = 2; i < nums.length; i++) {//从下标2运行到最后
            if (i % 2 == 0) {//判断单数偶数
                nums[i] = nums[i / 2];
            } else {
                nums[i] = nums[i / 2] + nums[i / 2 + 1];
            }
            if (nums[i] > max) {//记录最大值
                max = nums[i];
            }
        }
        return max;
    }
```



## [LCP 07. 传递信息](https://leetcode.cn/problems/chuan-di-xin-xi/)

### 问题

小朋友 A 在和 ta 的小伙伴们玩传信息游戏，游戏规则如下：

1. 有 n 名玩家，所有玩家编号分别为 0 ～ n-1，其中小朋友 A 的编号为 0
2. 每个玩家都有固定的若干个可传信息的其他玩家（也可能没有）。传信息的关系是单向的（比如 A 可以向 B 传信息，但 B 不能向 A 传信息）。
3. 每轮信息必须需要传递给另一个人，且信息可重复经过同一个人

给定总玩家数 `n`，以及按 `[玩家编号,对应可传递玩家编号]` 关系组成的二维数组 `relation`。返回信息从小 A (编号 0 ) 经过 `k` 轮传递到编号为 n-1 的小伙伴处的方案数；若不能到达，返回 0。

**示例 1：**

> 输入：`n = 5, relation = [[0,2],[2,1],[3,4],[2,3],[1,4],[2,0],[0,4]], k = 3`
>
> 输出：`3`
>
> 解释：信息从小 A 编号 0 处开始，经 3 轮传递，到达编号 4。共有 3 种方案，分别是 0->2->0->4， 0->2->1->4， 0->2->3->4。

**示例 2：**

> 输入：`n = 3, relation = [[0,2],[2,1]], k = 2`
>
> 输出：`0`
>
> 解释：信息不能从小 A 处经过 2 轮传递到编号 2

**限制：**

- `2 <= n <= 10`
- `1 <= k <= 5`
- `1 <= relation.length <= 90, 且 relation[i].length == 2`
- `0 <= relation[i][0],relation[i][1] < n 且 relation[i][0] != relation[i][1]`

### 答案

**思路**

注意动态规划重要的是找到dp数组之间的关系，经过k轮到编号n-1的次数，可以将问题最小化，逐步加大，找规律。

经过1轮到编号1的次数、2的次数、3的次数。。。n-1的次数。

经过2轮到编号1的次数、2的次数、3的次数。。。n-1的次数。

经过k轮到编号1的次数、2的次数、3的次数。。。n-1的次数。

列出表格，分析发现，第i轮编号j的次数=为第i-1轮 编号非j 进行到j编号可通的次数累计和。

注意：出入一定不要搞混了！！

**代码实现**

```java
public int numWays(int n, int[][] relation, int k) {
        boolean isConnect[][] = new boolean[n][n];
        //初试化可通数组，查询快
        for (int i = 0; i < relation.length; i++) {
            int[] temp = relation[i];
            isConnect[temp[0]][temp[1]] = true;//可通
        }
        //创建dp数组
        int[][] dp = new int[k][n];
        //初始化第1轮，记住下标从0开始为第1轮。
        for (int i = 0; i < n; i++) {
            if (isConnect[0][i]) {//如果从编号0能通则为1，默认0
                dp[0][i] = 1;
            }
        }
        for (int i = 1; i < k; i++) { //下标从0开始为第1轮，这里是第2轮，不做调整了，不影响
            for (int j = 0; j < n; j++) {//j代表i轮中到编号j
                for (int l = 0; l < n; l++) {//l遍历的是i-1轮中的元素
                    if (isConnect[l][j] && j != l) {//如果i-1轮中的编号->i轮当前编号有路，且不是当前编号，则累计种类
                        dp[i][j] += dp[i - 1][l];
                    }
                }

            }
        }
        //返回最后一个。
        return dp[k - 1][n - 1];
    }
```





## [LCR 003. 比特位计数](https://leetcode.cn/problems/w3tCBm/) 和338题重复

### 问题

给定一个非负整数 `n` ，请计算 `0` 到 `n` 之间的每个数字的二进制表示中 1 的个数，并输出一个数组。

 

**示例 1:**

```
输入: n = 2
输出: [0,1,1]
解释: 
0 --> 0
1 --> 1
2 --> 10
```

**示例 2:**

```
输入: n = 5
输出: [0,1,1,2,1,2]
解释:
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
```

 

**说明 :**

- `0 <= n <= 105`

 

**进阶:**

- 给出时间复杂度为 `O(n*sizeof(integer))` 的解答非常容易。但你可以在线性时间 `O(n)` 内用一趟扫描做到吗？
- 要求算法的空间复杂度为 `O(n)` 。
- 你能进一步完善解法吗？要求在C++或任何其他语言中不使用任何内置函数（如 C++ 中的 `__builtin_popcount` ）来执行此操作。

 

注意：本题与主站 338 题相同：https://leetcode-cn.com/problems/counting-bits/

### 答案

**思路**

找规划

0 --> 0
1 --> 1
2 --> 10  比 2-2多1
3 --> 11  比 3-2多1
4 --> 100   比4-4多1
5 --> 101  比5-4多1
...
n ===    比n- $2^i$多1



**代码实现**

```java
public int[] countBits(int n) {
        int[] dp = new int[n + 1];
        int max2 = 0;//记录最大的二进制位数
        for (int i = 1; i < dp.length; i++) {
            if ((i & (i - 1)) == 0) {//如果是最大二进位，则替换
                max2 = i;
            }
            dp[i] = dp[i - max2] + 1;//每次为之前的+1
        }

        return dp;
    }
```



后面也有重复的题就不列出来了。。。









## [LCR 161. 连续天数的最高销售额](https://leetcode.cn/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

### 问题

[LCR 161. 连续天数的最高销售额](https://leetcode.cn/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

简单



相关标签

相关企业



某公司每日销售额记于整数数组 `sales`，请返回所有 **连续** 一或多天销售额总和的最大值。

要求实现时间复杂度为 `O(n)` 的算法。

 

**示例 1:**

```
输入：sales = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：[4,-1,2,1] 此连续四天的销售总额最高，为 6。
```

**示例 2:**

```
输入：sales = [5,4,-1,7,8]
输出：23
解释：[5,4,-1,7,8] 此连续五天的销售总额最高，为 23。 
```

 

**提示：**

- `1 <= arr.length <= 10^5`
- `-100 <= arr[i] <= 100`

注意：本题与主站 53 题相同：https://leetcode-cn.com/problems/maximum-subarray/

### 答案

**思路**

找规律，可以参考官网解析，找出dp公式，做优化。

**代码实现**

```java
    public int maxSales(int[] sales) {
        int pre = sales[0];//记录前一个的最大价值
        int max = sales[0];//记录最大价值
        for (int i = 1; i < sales.length; i++) {//从下标1开始
            int temp = Math.max(pre + sales[i], sales[i]);//dp公式
            pre = temp;//记录前一个
            if (max < temp) {
                max = temp;//记录最大的
            }
        }
        return max;
    }
```



## [LCS 01. 下载插件](https://leetcode.cn/problems/Ju9Xwi/)

### 问题

小扣打算给自己的 **VS code** 安装使用插件，初始状态下带宽每分钟可以完成 `1` 个插件的下载。假定每分钟选择以下两种策略之一:

- 使用当前带宽下载插件
- 将带宽加倍（下载插件数量随之加倍）

请返回小扣完成下载 `n` 个插件最少需要多少分钟。

注意：实际的下载的插件数量可以超过 `n` 个

**示例 1：**

> 输入：`n = 2`
>
> 输出：`2`
>
> 解释： 以下两个方案，都能实现 2 分钟内下载 2 个插件
>
> - 方案一：第一分钟带宽加倍，带宽可每分钟下载 2 个插件；第二分钟下载 2 个插件
> - 方案二：第一分钟下载 1 个插件，第二分钟下载 1 个插件

**示例 2：**

> 输入：`n = 4`
>
> 输出：`3`
>
> 解释： 最少需要 3 分钟可完成 4 个插件的下载，以下是其中一种方案: 第一分钟带宽加倍，带宽可每分钟下载 2 个插件; 第二分钟下载 2 个插件; 第三分钟下载 2 个插件。

**提示：**

- `1 <= n <= 10^5`

### 答案

**思路**

这道题感觉用贪心算法，简单，动态规划可以自己参考官方。

找到一次运行就可以运行的数，最后加1次。

**代码实现**

```java
    public int leastMinutes(int n) {
        int times = 0;//当前运行次数
        int temp = 1;//默认每次处理1个
        while (temp<n) {//主要一直可以处理完就退出
            temp *= 2;
            times++;
        }
        return times + 1;//最后加一次安装
    }
```





## [面试题 05.03. 翻转数位](https://leetcode.cn/problems/reverse-bits-lcci/)

### 问题

给定一个32位整数 `num`，你可以将一个数位从0变为1。请编写一个程序，找出你能够获得的最长的一串1的长度。

**示例 1：**

```
输入: num = 1775(110111011112)
输出: 8
```

**示例 2：**

```
输入: num = 7(01112)
输出: 4
```

### 答案

**思路**

三遍历，分别记录没有包括0的长度、记录包含一个0的长度、记录最大长度。遇到0的时候重置。

**代码实现**

```java
    public int reverseBits(int num) {
        int cur = 0;//记录没有包括0的长度
        int insert = 0;//记录包含一个0的长度
        int max = 1;//记录最大长度
        for (int i = 0; i < 32; i++) {
            if ((num & (1 << i)) != 0) {//当前位置为1
                cur++;
                insert++;
            } else {
                insert = cur + 1;
                cur = 0;
            }
            if (insert > max) {
                max = insert;
            }
        }

        return max;
    }
```



## [面试题 08.01. 三步问题](https://leetcode.cn/problems/three-steps-problem-lcci/)

### 问题

三步问题。有个小孩正在上楼梯，楼梯有n阶台阶，小孩一次可以上1阶、2阶或3阶。实现一种方法，计算小孩有多少种上楼梯的方式。结果可能很大，你需要对结果模1000000007。

**示例1:**

```
 输入：n = 3 
 输出：4
 说明: 有四种走法
```

**示例2:**

```
 输入：n = 5
 输出：13
```

**提示:**

1. n范围在[1, 1000000]之间

### 答案

**思路**

同理70.爬楼梯

**代码实现**

```java
    public int waysToStep(int n) {
        if (n <= 1) return 1;
        if (n == 2) return 2;
        if (n == 3) return 4;
        int a = 1, b = 2, c = 4;
        for (int i = 4; i <= n; i++) {
            int temp = ((a + b)% 1000000007 + c)% 1000000007 ;
            a = b;
            b = c;
            c = temp;
        }
        return c;
    }
```



## [面试题 16.17. 连续数列](https://leetcode.cn/problems/contiguous-sequence-lcci/)

### 问题

给定一个整数数组，找出总和最大的连续数列，并返回总和。

**示例：**

```
输入： [-2,1,-3,4,-1,2,1,-5,4]
输出： 6
解释： 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

**进阶：**

如果你已经实现复杂度为 O(*n*) 的解法，尝试使用更为精妙的分治法求解。

### 答案

**思路**

同理LCR161.

**代码实现**

```java
    public int maxSubArray(int[] nums) {
        int pre = nums[0];
        int max = nums[0];
        for (int i = 1; i < nums.length; i++) {
            pre = Math.max(pre + nums[i], nums[i]);
            if (pre > max) {
                max = pre;
            }
        }

        return max;
    }
```



## [面试题 17.16. 按摩师](https://leetcode.cn/problems/the-masseuse-lcci/)

### 问题

一个有名的按摩师会收到源源不断的预约请求，每个预约都可以选择接或不接。在每次预约服务之间要有休息时间，因此她不能接受相邻的预约。给定一个预约请求序列，替按摩师找到最优的预约集合（总预约时间最长），返回总的分钟数。

**注意：**本题相对原题稍作改动

 

**示例 1：**

```
输入： [1,2,3,1]
输出： 4
解释： 选择 1 号预约和 3 号预约，总时长 = 1 + 3 = 4。
```

**示例 2：**

```
输入： [2,7,9,3,1]
输出： 12
解释： 选择 1 号预约、 3 号预约和 5 号预约，总时长 = 2 + 9 + 1 = 12。
```

**示例 3：**

```
输入： [2,1,4,5,3,1,1,3]
输出： 12
解释： 选择 1 号预约、 3 号预约、 5 号预约和 8 号预约，总时长 = 2 + 4 + 3 + 3 = 12。
```

### 答案

**思路**

查看官方解析，需要使用二维数组

**代码实现**

```java
    public int massage(int[] nums) {
        if (nums.length == 0) return 0;
        if (nums.length == 1) return nums[0];
        if (nums.length == 2) return nums[0] > nums[1] ? nums[0] : nums[1];

        int[][] dp = new int[nums.length][2];//第二维，0代表不按，1代表按
        dp[0][0] = 0;
        dp[0][1] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            dp[i][0] = Math.max(dp[i - 1][1], dp[i - 1][0]);//如果第i次不按，选则i-1按和不按中的一个最大值
            dp[i][1] = dp[i - 1][0] + nums[i];//如果i次按，则前一次的不按，加上当前值
        }
        return Math.max(dp[nums.length - 1][0], dp[nums.length - 1][1]);//选择最大的。
    }
```













## template

### 问题



### 答案

**思路**



**代码实现**



# 中等

## [5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring/)

### 问题

给你一个字符串 `s`，找到 `s` 中最长的回文子串。

如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。

 

**示例 1：**

```
输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
```

**示例 2：**

```
输入：s = "cbbd"
输出："bb"
```

 

**提示：**

- `1 <= s.length <= 1000`
- `s` 仅由数字和英文字母组成

### 答案

**思路**

看官方解析，中等难度已经有些困难了。。。冲

**代码实现**

```java
    public String longestPalindrome(String s) {
        if (s.length() <= 1) {//长度小于1默认为回文
            return s;
        }
        int n = s.length();
        boolean[][] dp = new boolean[n][n];//i->j是不是回文串，i<=j
        for (int i = 0; i < n; i++) {//i->i是回文
            dp[i][i] = true;
        }
        int begin = 0;//默认从0开始
        int maxLen = 1;//默认1为最大长度
        for (int i = 0; i < n - 1; i++) {//判断长度为2的是否为回文数
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                begin = i;
                maxLen = 2;
            }
        }

        for (int L = 2; L < n; L++) {//当前子字串长度 1+L  例如0->2 长度为3
            for (int i = 0; i < n - L; i++) { //i表示头
                //dp[i + 1][i + L - 1] 头和尾缩减1是否为回文
                //s.charAt(i) == s.charAt(i + L) 头和尾是否相同
                if (dp[i + 1][i + L - 1] && s.charAt(i) == s.charAt(i + L)) {
                    dp[i][i + L] = true;//满足以上两条件则当前也是回文
                    if (L + 1 > maxLen) {//！！长度一定记得L+1
                        maxLen = L + 1;
                        begin = i;
                    }
                }
            }
        }
        //截取字符串
        return s.substring(begin, begin + maxLen);
    }
```





## [22. 括号生成-待优化-回溯法！！！！](https://leetcode.cn/problems/generate-parentheses/)

### 问题

数字 `n` 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 **有效的** 括号组合。

 

**示例 1：**

```
输入：n = 3
输出：["((()))","(()())","(())()","()(())","()()()"]
```

**示例 2：**

```
输入：n = 1
输出：["()"]
```

 

**提示：**

- `1 <= n <= 8`

### 答案

**思路**

使用set去重，运行时间很长代替待优化。

**代码实现**

```java
    public List<String> generateParenthesis(int n) {
        Set<String> set = new HashSet<>();
        set.add("()");
        for (int i = 1; i < n; i++) {
            Set<String> setTemp = new HashSet<>();
            set.stream().forEach(item -> {
                for (int j = 0; j <= item.length(); j++) {//每次把()加入中间
                    setTemp.add(item.substring(0,j)+"()"+item.substring(j,item.length()));
                }
            });
            set = setTemp;
        }
        return set.stream().toList();
    }
```



## [45. 跳跃游戏 II](https://leetcode.cn/problems/jump-game-ii/)

### 问题

给定一个长度为 `n` 的 **0 索引**整数数组 `nums`。初始位置为 `nums[0]`。

每个元素 `nums[i]` 表示从索引 `i` 向前跳转的最大长度。换句话说，如果你在 `nums[i]` 处，你可以跳转到任意 `nums[i + j]` 处:

- `0 <= j <= nums[i]` 
- `i + j < n`

返回到达 `nums[n - 1]` 的最小跳跃次数。生成的测试用例可以到达 `nums[n - 1]`。

 

**示例 1:**

```
输入: nums = [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。
```

**示例 2:**

```
输入: nums = [2,3,0,1,4]
输出: 2
```

 

**提示:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 1000`
- 题目保证可以到达 `nums[n-1]`

### 答案

**思路**

方法一，自己想的，每经过一个格子则更新里面的最小次数。

方法二，官方解析，正向查找可到达的最大位置

**代码实现**

方法一：

```java
    public int jump(int[] nums) {
        int[] cost = new int[nums.length];//次数
        for (int i = 1; i < nums.length; i++) {
            cost[i] = nums.length;//设置最大跳数。
        }
        for (int i = 0; i < nums.length - 1; i++) {//遍历除了最后一个
            for (int j = i + 1; j <= i + nums[i] && j < nums.length; j++) {//当前的后面一个 到 可以跳的最后一个
                cost[j] = Math.min(cost[j], cost[i]+1);//更新最小值
                if (j >= nums.length) {//如果到了最后一个，则找到最小的
                    return cost[nums.length - 1];
                }
            }
        }
        return cost[nums.length - 1];
    }
```

方法二

```java
    public int jump(int[] nums) {
        int end = 0;//每一轮的最后一个
        int maxPosition = 0;//当前最大可以跳到的位置
        int step = 0;//步数
        for (int i = 0; i < nums.length - 1; i++) {//最后一个不需要遍历
            maxPosition = Math.max(maxPosition, i + nums[i]);
            if (i == end) {
                end = maxPosition;
                step++;
            }
        }
        return step;
    }
```



## [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

### 问题

给你一个整数数组 `nums` ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**子数组** 是数组中的一个连续部分。

 

**示例 1：**

```
输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
```

**示例 2：**

```
输入：nums = [1]
输出：1
```

**示例 3：**

```
输入：nums = [5,4,-1,7,8]
输出：23
```

 

**提示：**

- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

 

**进阶：**如果你已经实现复杂度为 `O(n)` 的解法，尝试使用更为精妙的 **分治法** 求解。

### 答案

**思路**

dp[i] = max(dp[i-1]+nums[i],nums[i])

**代码实现**

```java
    public int maxSubArray(int[] nums) {
        if (nums.length == 1) {
            return nums[0];
        }
        int preMax = nums[0];
        int AllMax = nums[0];
        for (int i = 1; i < nums.length; i++) {
            preMax = Math.max(preMax + nums[i], nums[i]);
            if (preMax > AllMax) {
                AllMax = preMax;
            }
        }

        return AllMax;
    }
```





## [55. 跳跃游戏](https://leetcode.cn/problems/jump-game/)

### 问题

给你一个非负整数数组 `nums` ，你最初位于数组的 **第一个下标** 。数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标，如果可以，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

```
输入：nums = [2,3,1,1,4]
输出：true
解释：可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。
```

**示例 2：**

```
输入：nums = [3,2,1,0,4]
输出：false
解释：无论怎样，总会到达下标为 3 的位置。但该下标的最大跳跃长度是 0 ， 所以永远不可能到达最后一个下标。
```

 

**提示：**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 105`

### 答案

**思路**

和45.跳跃游戏II思路一样。记得考虑边界情况

**代码实现**

```java
    public boolean canJump(int[] nums) {
        int curPosition = 0;//当前能到的最大位置
        for (int i = 0; i <= curPosition && i < nums.length; i++) {//每次只能跳到最大的位置
            if (i + nums[i] > curPosition) {//如果当前最远位置大
                curPosition = i + nums[i];//更新
                if (curPosition >= nums.length - 1) {//如果到了最后一个退出
                    return true;
                }
            }
        }

        return false;
    }
```



## [62. 不同路径](https://leetcode.cn/problems/unique-paths/)

### 问题

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？

 

**示例 1：**

![img](https://pic.leetcode.cn/1697422740-adxmsI-image.png)

```
输入：m = 3, n = 7
输出：28
```

**示例 2：**

```
输入：m = 3, n = 2
输出：3
解释：
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右
3. 向下 -> 向右 -> 向下
```

**示例 3：**

```
输入：m = 7, n = 3
输出：28
```

**示例 4：**

```
输入：m = 3, n = 3
输出：6
```

 

**提示：**

- `1 <= m, n <= 100`
- 题目数据保证答案小于等于 `2 * 109`

### 答案

**思路**

​	没有想出来，参考leetcode官方解释

**代码实现**

```java
    public int uniquePaths(int m, int n) {
        if (m == 1 || n == 1) return 1;
        int nmax, nmin;//因为m = 3, n=2;n=3,m=2  互换位置结果不变。
        if (m > n) {
            nmax = m;
            nmin = n;
        } else {
            nmax = n;
            nmin = m;
        }
	//这里有个错误，应该选择小的nmin，可以省空间，自己修改一下。
        int[] dp = new int[nmax];
        for (int i = 0; i < nmax; i++) {//初试化第一行
            dp[i] = 1;
        }
        for (int i = 1; i < nmin; i++) {//从第二行开始
            for (int j = 1; j < nmax; j++) {//遍历列
                dp[j] = dp[j - 1] + dp[j];//画个图就可以理解了，dp[j-1]表示左边的，dp[j] 因为还是记录上一行的，直接加
            }
        }
        return dp[nmax-1];
    }
```



## [63. 不同路径 II](https://leetcode.cn/problems/unique-paths-ii/)

### 问题

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 `1` 和 `0` 来表示。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)

```
输入：obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
输出：2
解释：3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg)

```
输入：obstacleGrid = [[0,1],[0,0]]
输出：1
```

 

**提示：**

- `m == obstacleGrid.length`
- `n == obstacleGrid[i].length`
- `1 <= m, n <= 100`
- `obstacleGrid[i][j]` 为 `0` 或 `1`

### 答案

**思路**

和62.不同路径一样，只不过需要把有阻挡的位置清零。

**代码实现**

```java
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
//        if (obstacleGrid==null||obstacleGrid.length==0) return 0;//题目已经限制了不需要判断
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;

        int[] dp = new int[n];//记录列
        if (obstacleGrid[0][0] != 1) {//判断第一个位置有没有占位
            dp[0] = 1;
        } else {
            return 0;//如果第一个就占，肯定过不去
        }
        for (int i = 0; i < m; i++) {//从第1行开始
            for (int j = 0; j < n; j++) {//遍历列
                if (j != 0) {//第一个左边没有要特殊处理
                    //画个图就可以理解了，dp[j-1]表示左边的，dp[j] 因为还是记录上一行的，直接加
                    //如果被挡住了，直接直接为0
                    dp[j] = obstacleGrid[i][j] == 0 ? dp[j - 1] + dp[j] : 0;
                } else {
                    dp[j] = obstacleGrid[i][j] == 0 ? dp[j] : 0;
                }
            }
        }
        return dp[n - 1];
    }
```



## [64. 最小路径和](https://leetcode.cn/problems/minimum-path-sum/)

### 问题

给定一个包含非负整数的 `*m* x *n*` 网格 `grid` ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

**说明：**每次只能向下或者向右移动一步。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

```
输入：grid = [[1,3,1],[1,5,1],[4,2,1]]
输出：7
解释：因为路径 1→3→1→1→1 的总和最小。
```

**示例 2：**

```
输入：grid = [[1,2,3],[4,5,6]]
输出：12
```

 

**提示：**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 200`
- `0 <= grid[i][j] <= 200`

### 答案

**思路**

同上一题思路，只不过，把路径和相加，先判断谁小，再加当前的值。

**代码实现**

```java
    public int minPathSum(int[][] grid) {
        int m = grid.length;//行
        int n = grid[0].length;//列
        int[] dp = new int[n];
        int sum = 0;
        for (int i = 0; i < n; i++) {//初始化第一行的费用
            sum += grid[0][i];//第一行第i列的费用。
            dp[i] = sum;
        }
        for (int i = 1; i < m; i++) {//从第二开始
            for (int j = 0; j < n; j++) {
                if (j == 0) {//下标为0 特殊处理
                    dp[j] = dp[j] + grid[i][j];
                } else {
                    dp[j] = Math.min(dp[j], dp[j - 1]) + grid[i][j];
                }
            }
        }
        return dp[n - 1];
    }
```













## template

### 问题



### 答案

**思路**



**代码实现**



