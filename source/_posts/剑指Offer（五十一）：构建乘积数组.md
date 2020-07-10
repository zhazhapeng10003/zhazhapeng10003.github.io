---
title: 剑指Offer（五十一）：构建乘积数组
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
abbrlink: 30060
date: 2020-04-02 00:54:23
coverImg:
tags:
  - 剑指Offer
  - 数组
categories: 刷题
password:
---


## 构建乘积数组:
#### 题目链接：
[牛客网](https://www.nowcoder.com/practice/94a4d381a68b47b7a8bed86f2975db46?tpId=13&tqId=11204&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。（注意：规定B[0]=A[0]×A[1]×…×A[n-2];）<br/>
**<font size = 3 face= '黑体'>示例 1：**
>**输入:** [1,2,3,4,5]
**输出:** [120,60,40,30,24]

**<font size = 3 face= '黑体'>示例 2：**
>**输入:** [2,2,2,0,1]
**输出:** 1

#### 解题思路：<br/>
因为题目要求不能使用除法，所以我们不能使用公式 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1] 表示,使用除法时要特别注意A[i]等于0的情况。

![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvMTQwNzMzMC8yMDE4MTEvMTQwNzMzMC0yMDE4MTExNjIxNDYzNTc0OC0xOTY4NzQwODU1LnBuZw?x-oss-process=image/format,png#pic_center)
（图片转自[此处](https://www.cnblogs.com/wxdjss/p/5448990.html)）
**<font size = 3>•** 从图中可以发现，B[i] 的左半部分与 B[i-1] 有关（**B[i] = B[i-1] * A[i-1]**）;
**<font size = 3>•** 把 B[i] 的右半部分看作D[i]，有D[i] = D[i+1] * A[i+1]；<br>
**<font size = 3>•** 因此我们先从0到n-1遍历，计算每个B[i]的左半部分；然后定义一个变量 temp 代表右半部分的乘积，从 n-1 到 0 遍历，令 B[i]* = temp，而每次的 temp 与上次的 temp 关系即为temp* = A[i+1]。
#### 复杂度：<br/>
时间复杂度：***O*(N)**

#### 代码实现：<br/>
```java
import java.util.ArrayList;
public class Solution {
    public int[] multiply(int[] A) {
        if (A == null || A.length == 0){
            return new int[0];
        }

        int[] B = new int[A.length];
        B[0] = 1;
        for (int i = 1; i < A.length; i++){
            B[i] = B[i - 1] * A[i - 1];
        }
        int temp = 1;
        for (int i = A.length - 2; i >= 0; i--){
            temp *= A[i+1];
            B[i] *= temp;
        }
        return B;
    }
}
```
<font size = 5>**Peace!**
