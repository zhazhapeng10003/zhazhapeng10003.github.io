---
title: 剑指Offer（六十四）：滑动窗口的最大值
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
abbrlink: 64066
date: 2020-04-02 01:03:18
coverImg:
tags:
  - 剑指Offer
  - 数组
categories: 刷题
password:
---


## 滑动窗口的最大值:
#### 题目链接：
[牛客网](//www.nowcoder.com/practice/1624bc35a45c42c0bc17d17fa0cba788?tpId=13&tqId=11217&tPage=4&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}； 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}，
 {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。<br/>
**<font size = 3>示例 1：**
>**输入:** nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
**输出:** [3,3,5,5,6,7] 
 滑动窗口的位置&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;                &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;最大值
>-----------------------------------        &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;-----
>[1 &ensp; 3&ensp;  -1] &ensp;-3  &ensp;5 &ensp; 3&ensp;  6  &ensp;7   &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;3
 1&ensp; [3 &ensp;-1 &ensp; -3] &ensp;5  &ensp;3 &ensp; 6 &ensp;7 &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;3
 1  &ensp;3&ensp; [-1  &ensp;-3  &ensp;5] &ensp;3 &ensp; 6  &ensp;7&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;5
 1  &ensp;3 &ensp; -1&ensp; [-3 &ensp; 5  &ensp;3] &ensp;6 &ensp;7&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;5
 1  &ensp;3 &ensp; -1  &ensp;-3&ensp; [5  &ensp;3&ensp;  6] &ensp;7&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;6
 1 &ensp; 3 &ensp; -1  &ensp;-3&ensp;  5&ensp; [3 &ensp; 6&ensp;  7]  &ensp;&ensp;&ensp;&ensp;&ensp;7

#### 解题思路：<br/>
&ensp;&ensp;&ensp;&ensp;利用双端队列：
**<font size = 3>•** 每次 push 时，从队尾把值加进来。加进来的同时判断从右到左判断，比他小与等于的值全部弹出；
**<font size = 3>•** 队头每次向右移动 ，判断队头的坐标是否过期。（越界）越界的话就弹出。
#### 复杂度：<br/>
时间复杂度：***O*(N)**，每个元素被处理两次- 其索引被添加到双向队列中和被双向队列删除
空间复杂度：***O*(N)**，双向队列的空间


#### 代码实现：<br/>
```java
import java.util.ArrayList;
import java.util.Deque;
import java.util.LinkedList;
public class JianZhiOffer64 {
    public static ArrayList<Integer> maxInWindows(int[] num, int size){
        if (num == null || num.length == 0 || size > num.length) return null;
        ArrayList<Integer> result = new ArrayList<>();
        Deque<Integer> deque = new LinkedList<>();


        for (int j = 0; j < num.length; j++) {
            //如果队头元素不在滑动窗口中，就删除头元素；
            while (!deque.isEmpty() && j >= deque.getFirst() + size) {
                deque.pollLast();
            }

            //如果当前元素大于队尾则删除
            while (!deque.isEmpty() && num[j] > num[deque.getLast()]) {
                deque.pollLast();
            }

            deque.offer(j);

            if (j + 1 >= size) {
                result.add(deque.peek());
            }
        }
        return result;
    }
}

```
<font size = 5>**Peace!**
