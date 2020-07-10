---
title: 剑指Offer（十三）：调整数组顺序使奇数位于偶数前面
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
tags:
  - 剑指Offer
  - 数组
categories: 刷题
abbrlink: 45411
date: 2020-04-01 23:40:11
coverImg:
password:
---


## 调整数组顺序使奇数位于偶数前面:
#### 题目链接：
[牛客网](//www.nowcoder.com/practice/beb5aa231adc45b2a5dcc5b62c93f593?tpId=13&tqId=11166&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。<br/>
**示例 1：**
>**输入：** nums = [1,2,3,4]
**输出：** [1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。

#### 解题思路：<br/>
###### 解法1：
遍历原数组，分别取出奇偶数放入新的数组，再放回原数组：
#### 复杂度：<br/>
时间复杂度：***O*(2N)** ，N为数组长度
空间复杂度：***O*(2N)**， N为数组长度
#### 代码实现：<br/>
```java
public static void ReOrderArr(int[] arr){
    ArrayList<Integer> odd  = new ArrayList<>();
    ArrayList<Integer> even  = new ArrayList<>();
    for (int i = 0; i < arr.length; i++){
        if (arr[i] % 2 == 1){
            odd.add(arr[i]);
        }
        else even.add(arr[i]);
    }
    for (int i = 0; i < odd.size(); i++){
        arr[i] = odd.get(i);
    }
    for (int i = 0; i < even.size(); i++){
        arr[odd.size() + i] = even.get(i);
    }
}
```
###### 解法2（双指针法简洁版）：
利用 <font color = red>**快慢双指针** <font color = black>遍历原数组，快指针对应的数若为奇数，则与慢指针对应数交换，不需要额外开辟内存空间。
#### 复杂度：<br/>
时间复杂度：***O*(N)** ，N为数组长度
空间复杂度：***O*(1)**
#### 代码实现：<br/>
```java
public int[] exchange(int[] nums) {
    if (nums.length == 0) {
        return new int[0];
    }
    int start = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] % 2 == 1) {
            int temp = nums[i];
            nums[i] = nums[start];
            nums[start] = temp;
            start++;
        }
    }
    return nums;
}
```
<font size = 5>**Peace!**
