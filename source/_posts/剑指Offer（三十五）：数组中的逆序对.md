---
title: 剑指Offer（三十五）：数组中的逆序对
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
abbrlink: 35899
date: 2020-04-02 00:26:48
coverImg:
tags:
  - 剑指Offer
  - 数组
categories: 刷题
password:
---

## 数组中的逆序对:
#### 题目链接：
[牛客网](//www.nowcoder.com/practice/96bd6684e04a44eb80e6a68efc0ec6c5?tpId=13&tqId=11188&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007<br/>
**<font size = 3>示例 1：**
>**输入:** [7,5,6,4]
**输出:** 5
#### 解题思路：<br/>
&ensp;&ensp;&ensp;&ensp;每一个值都要跟前面的值进行比较判断是否为逆序对，可以借助归并排序，利用 <font color = red>分治<font color = black>的思想，在排序的过程中统计逆序对。
逆序对的来源：
**<font size = 3>•** 左边区间的逆序对
**<font size = 3>•** 右边区间的逆序对
**<font size = 3>•** 横跨两个区间的逆序对
**<font size = 3>•** 即：[A，B]中的逆序对 = [A]的逆序对 + [B]中的逆序对 + 将A，B混排在一起的逆序对
#### 复杂度：<br/>
时间复杂度：***O*(NlogN)**

#### 代码实现：<br/>
```java
public class JianZhiOffer35 {
    public int count = 0;

    public int InversePairs(int[] array){
        MergeSort(array, 0, array.length - 1);
        return count;
    }

    public void MergeSort(int[] array, int left, int right){
        if (left < right){
            int mid = (left + right) >> 1;
            MergeSort(array, left, mid);
            MergeSort(array, mid + 1, right);
            Merge(array, left, mid, right);
        }
    }

    public void Merge(int[] array, int left, int mid, int right){
        int[] temp = new int[right - left + 1];
        int k = 0, i = left, j = mid + 1;
        while (i <= mid && j <= right){
        	//如果前面的元素小于后面的不能构成逆序对
            if (array[i] <= array[j]){
                temp[k++] = array[i++];
            }
            //如果前面的元素大于后面的，那么在前面元素之后的元素都能和后面的元素构成逆序对
            else {
                temp[k++] = array[j++];
                count += mid - i + 1;
                count = count % 1000000007;//在leetcode中，此行不加
            }
        }

        while (i <= mid){
            temp[k++] = array[i++];
        }

        while (j <= mid){
            temp[k++] = array[i++];
        }

        for(int l=0; l<k; l++){
            array[left+l] = temp[l];
        }
    }
}
```
<font size = 5>**Peace!**

