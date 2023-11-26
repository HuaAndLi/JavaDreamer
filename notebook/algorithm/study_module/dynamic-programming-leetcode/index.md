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





## template

### 问题



### 答案

**思路**



**代码实现**







