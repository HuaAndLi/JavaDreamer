## 简介 

《算法图解》笔记

# 第一章

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

### 1.1 假设有一个包含128个名字的有序列表，你要使用二分查找在其中查找一个名字，请 问最多需要几步才能找到？ 

log(128) = 7

### 1.2 上面列表的长度翻倍后，最多需要几步？

8

### 1.3 在电话簿中根据名字查找电话号码。 使用大O表示法给出下述各种情形的运行时间。

根据字母姓式二分查找所用时间为:O(log n)

### 1.4 在电话簿中根据电话号码找人。（提示：你必须查找整个电话簿。） 

简单查找，所用时间为:O(n)

### 1.5 阅读电话簿中每个人的电话号码。 

简单查找，所用时间为：O(n)

### 1.6 阅读电话簿中姓名以A打头的人的电话号码。这个问题比较棘手，它涉及第4章的概 念。答案可能让你感到惊讶！

简单查找，所用时间为：O(n)