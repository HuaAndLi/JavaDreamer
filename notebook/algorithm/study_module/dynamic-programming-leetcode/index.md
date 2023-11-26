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







