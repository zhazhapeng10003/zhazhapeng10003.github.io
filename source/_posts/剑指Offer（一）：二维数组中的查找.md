---
title: 剑指Offer（一）：二维数组中的查找
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
coverImg: 
toc: true
mathjax: true
comments: true
summary: ' '
tags:
  - 剑指Offer
  - 数组
categories: 刷题
abbrlink: 43262
date: 2020-03-29 23:36:45
password:
---

## 二维数组中的查找:
#### 题目链接：
[牛客网](https://www.nowcoder.com/practice/abc3fe2ce8e146608e868a70efebf62e?tpId=13&tqId=11154&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。<br/>

>Consider the following matrix:
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

Given target = ```5```, return ```true```。
Given target = ```20```, return ```false```。<br/>
#### 解题思路：<br/>

利用该二维数组的性质：

**<font size = 3>•** 每一行都按照从左到右递增的顺序排序，
**<font size = 3>•** 每一列都按照从上到下递增的顺序排序
&ensp;&ensp;&ensp;&ensp;该二维数组中的一个数，小于它的数一定在其左边，大于它的数一定在其下边。因此，从右上角开始查找，就可以根据 target 和当前元素的大小关系来缩小查找区间，当前元素的查找区间为左下角的所有元素。<br/>
**<font size = 3>•** 当 m < target，由于 m 已经是该行最大的元素，想要更大只有从列考虑，取值右移一位
**<font size = 3>•** 当 m > target，由于 m 已经是该列最小的元素，想要更小只有从行考虑，取值上移一位
**<font size = 3>•** 当 m = target，找到该值，返回 true
用某行最小或某列最大与 target 比较，每次可剔除一整行或一整列。<br/>
<center>
<img src="https://img-blog.csdnimg.cn/20200322183416116.gif" width="50%"> <br/>
</center>

#### 复杂度：<br/>
时间复杂度：***O*(行高+列宽)**
空间复杂度：***O*(1)**
#### 代码实现：<br/>
```java
public class Solution {
    public boolean Find(int target, int [][] array) {
        int i = array.length - 1;
        int j = 0;
        int value = target;
        while (i >= 0 && j < array[0].length){
            if (array[i][j] < value){
                j++;
            }else if (array[i][j] > value){
                i--;
            }else {
                return true;
            }
        }
        return false;
    }
}
```
<font size = 5>**Peace!**




