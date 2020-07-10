---
title: 剑指Offer（六）：旋转数组的最小数字
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
abbrlink: 27960
date: 2020-04-01 23:19:50
coverImg:
password:
---



## 旋转数组的最小数字:
#### 题目链接：
[牛客网](//www.nowcoder.com/practice/9f3231a991af4f55b95579b44b7a01ba?tpId=13&tqId=11159&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。<br/>
**示例 1：**
>**输入:** [1,3,5]
**输出:** 1

**示例 2：**
>**输入:** [2,2,2,0,1]
**输出:** 1

#### 解题思路：<br/>
将旋转数组对半分可以得到一个包含最小元素的新旋转数组，以及一个非递减排序的数组。新的旋转数组的数组元素是原数组的一半，从而将问题规模减少了一半，这种折半性质的算法的时间复杂度***O*(logN)**。

**•** 取数组 arr 的**left、right、mid =（left + right）/ 2**；
**•** 情况1：如果arr[left] < arr[right]，说明该旋转数组是有序数组，最小值即为arr[left]；
**•** 情况2：array[left] < array[mid]，说明左半部分是有序的，我们应该在右半部分找最小值，令==left = mid + 1==；
**•** 情况3：array[right] > array[mid]，说明右半部分是有序的，为防止漏掉最小值，==right = mid== 而不是 right = mid-1；
**•** 情况4：其他特殊情况不满足条件，如arr[left] = arr[right]，array[left] = array[mid]，不好判断，==left++==，向右缩小范围继续判断。

#### 复杂度：<br/>
时间复杂度：***O*(logN)**

#### 代码实现：<br/>
```java
public class Solution {
    public static int minNumberInRotateArray(int[] array){
        if (array.length == 0) return 0;
        int left = 0;
        int right = array.length - 1;
        while (left < right){
            int mid = (left + right) / 2;
            //说明数组是有序数组
            if (array[left] < array[right]){
                return array[left];
            }
            //左半部分是有序的，其最小值肯定在右半部分
            if (array[left] < array[mid]){
                left = mid + 1;
            }
            //右半部分是有序的，为防止漏掉最小值，right = mid 而不是 right = mid-1
            else if (array[right] > array[mid]){
                right = mid;
            }
            //向右缩小范围继续判断
            else left++;
        }
        return array[left];
	}
}
```
<font size = 5>**Peace!**
