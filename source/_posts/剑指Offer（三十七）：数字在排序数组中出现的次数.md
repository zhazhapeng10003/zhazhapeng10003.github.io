---
title: 剑指Offer（三十七）：数字在排序数组中出现的次数
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
abbrlink: 12141
date: 2020-04-02 00:34:42
coverImg:
tags:
  - 剑指Offer
  - 数组
categories: 刷题
password:
---


## 数字在排序数组中出现的次数:
#### 题目链接：
[牛客网](//www.nowcoder.com/practice/70610bf967994b22bb1c26f9ae901fa2?tpId=13&tqId=11190&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;统计一个数字在排序数组中出现的次数。<br/>
**<font size = 3>示例 1：**
>**输入:** nums = [5,7,7,8,8,10], target = 8
**输出:** 2

**<font size = 3>示例 2：**
>**输入:** nums = [5,7,7,8,8,10], target = 6
**输出:** 0

#### 解题思路：<br/>
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** 可以先二叉搜索找一下这个元素的位置，然后再开始遍历搜索一下。
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** 或者利用二分法进行求解，因为是排序数组，可以找到 target 的左边界 left 和有边界 right，<font color = red>**righ - left - 1**<font color = black>即为数字出现的次数
#### 复杂度：<br/>
时间复杂度：***O*(logN)**
注：如果整个数组都是 target 的话，第一种会退化成***O*(logN)**

#### 代码实现：<br/>
```java
import java.util.Arrays;
public class Solution {
    public int GetNumberOfK(int [] array , int k) {
        int index = Arrays.binarySearch(array, k);
        if (index < 0) {
            return 0;
        }
        int count = 1;
        for (int i = index + 1; i < array.length && array[i] == k; ++i){
            count++;
        }
        for (int i = index - 1; i >=0 && array[i] == k; --i){
            count++;
        }
        return count;
    }
}
```

```java
class Solution {
    public int search(int[] nums, int target) {
        int i = 0, j = nums.length - 1;
        while(i <= j) {
            int m = (i + j) / 2;
            if(nums[m] <= target) i = m + 1;
            else j = m - 1;
        }
        int right = i;

        i = 0; j = nums.length - 1;
        while(i <= j) {
            int m = (i + j) / 2;
            if(nums[m] < target) i = m + 1;
            else j = m - 1;
        }
        int left = j;
        
        return right - left - 1;
    }
}
```

<font size = 5>**Peace!**
