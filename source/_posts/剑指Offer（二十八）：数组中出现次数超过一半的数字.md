---
title: 剑指Offer（二十八）：数组中出现次数超过一半的数字
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
abbrlink: 38908
date: 2020-04-02 00:30:22
coverImg:
tags:
  - 剑指Offer
  - 数组
categories: 刷题
password:
---


## 数组中出现次数超过一半的数字:
#### 题目链接：
[牛客网](https://www.nowcoder.com/practice/e8a1b01a2df14cb2b228b30ee6a92163?tpId=13&tqId=11181&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。<br/>
**<font size = 3 face= '黑体'>示例 1：**
>**输入:** [1, 2, 3, 2, 2, 2, 5, 4, 2]
**输出:** 2

**<font size = 3 face= '黑体'>示例 2：**
>**输入:** [2,2,1,1,1,2,2]
**输出:** 2

#### 解题思路：<br/>
采用阵地攻守的思想：
**<font size = 3>•** 第一个数字作为第一个士兵，守阵地；**count = 1**；
**<font size = 3>•** 遇到相同元素，**count++**;
**<font size = 3>•** 遇到不相同元素，即为敌人，同归于尽，**count--**；当遇到count为0的情况，又以新的i值作为守阵地的士兵，继续下去，到最后还留在阵地上的士兵，有可能是主元素。
**<font size = 3>•** 再加一次循环，记录这个士兵的个数看是否大于数组一般即可。



#### 复杂度：<br/>
时间复杂度：***O*(N)**

#### 代码实现：<br/>
**<font size = 3>•** ==注：== length / 2 用 **length >> 1** 代替进行运算效率更高~
```java
public class Solution {
    public int MoreThanHalfNum_Solution(int[] array){
        if (array == null || array.length == 0) return 0;
        int preValue = array[0];//当前阵地中的士兵
        int count = 1;//阵地中士兵的数量
        for (int i = 1; i < array.length; i++){
        	//如果是相同阵营的士兵则数量+1
            if (array[i] == preValue){
                count++;
            }
            //与敌人同归于尽，数量-1
            else {
                count--;
                //士兵全部阵亡，取新的当前值作为守阵士兵
                if (count == 0){
                    preValue = array[i];
                    count = 1;
                }
            }
        }
		//判断这个士兵是不是真的是数量大于一半
        int num = 0;
        for (int i = 0; i < array.length; i++){
            if (array[i] == preValue){
                num++;
            }
        }
        return (num > array.length/2)?preValue:0;
    }
}
```
<font size = 5>**Peace!**
