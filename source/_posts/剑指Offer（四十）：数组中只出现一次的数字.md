---
title: 剑指Offer（四十）：数组中只出现一次的数字
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
abbrlink: 46036
date: 2020-04-02 00:39:39
coverImg:
tags:
  - 剑指Offer
  - 数组
categories: 刷题
password:
---

## 数组中只出现一次的数字:
#### 题目链接：
[牛客网](//www.nowcoder.com/practice/e02fdb54d7524710a7d664d082bb7811?tpId=13&tqId=11193&tPage=2&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。<br/>
**<font size = 3>示例 1：**
>**输入:** [1,2,1,3,2,5]
**输出:** [3,5]

#### 解题思路：<br/>
**<font size = 3>•** （一）：用利用哈希表的特性来解答
**<font size = 3>•** （二）：利用异或：<br/>
&ensp;&ensp;&ensp;&ensp;现在数组中只有连个数字只出现过1次 a, b ，直接异或一次只能得到这两个数字的异或结果。如果我们把这两个数字分到两个数组当中，再让两个分组各自进行异或，那么就能得到结果了。
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** **关键：** 如何将这两个数字分开到两个数组当中。
&ensp;&ensp;&ensp;&ensp;由于 a, b 肯定是不相等的，那么在二进制上肯定有一位是不同的。**根据这一位是 0 还是 1 可以将 a，b 分成 a组和 b组。** 而这个数组中其它数字不是属于 a组就是 b组。再对a，b组进行异或就能得到 a、b了。**根据 a、b异或的结果我们可以得知，结果的二进制中 ‘1’ 的位就说明 a、b在这一位上是不同的。**
>int nums[ ] = {1, 1, 3, 5, 2, 2}

整个数组异或的结果为3^5，即 0x0011 ^ 0x0101 = 0x0110；
对 0x0110，第1位（由低向高，从0开始）就是1，整个数组根据第1位是0还是1分成两组。
>nums[0] = 1  0x0001  第一组<br>
>nums[1] = 1  0x0001  第一组<br>
>nums[2] = 3  0x0011  第二组<br>
>nums[2] = 3  0x0011  第二组<br>
>nums[3] = 5  0x0101  第一组<br>
>nums[4] = 2  0x0010  第二组<br>
>nums[5] = 2  0x0010  第二组<br>
#### 复杂度：<br/>
方法（一）
时间复杂度：***O*(N)**
空间复杂度：***O*(N)**，哈希表所使用的空间。<br>
方法（二）：
时间复杂度：***O*(N)**
空间复杂度：***O*(1)**


#### 代码实现：<br/>
方法一：
```java
//num1,num2分别为长度为1的数组。传出参数
//将num1[0],num2[0]设置为返回结果
import java.util.HashMap;
public class Solution {
    public void FindNumsAppearOnce(int [] array,int num1[] , int num2[]) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < array.length; ++i){
            if (map.containsKey(array[i])){
                map.put(array[i], 2);
            }
            else {
                map.put(array[i], 1);
            }
        }
        int count = 0;
        for (int i = 0; i < array.length; ++i){
            if (map.get(array[i]) == 1){
                if (count == 0){
                    num1[0] = array[i];
                    count++;
                }
                else {
                    num2[0] = array[i];
                }
            }
        }
    }
}
```
方法二：

```java
class Solution {
    public int[] singleNumber(int[] nums) {
        int [] res = new int [2];
        if (nums == null || nums.length < 2) {
            return res;
        }
        int xorRes = 0;
        for (int x : nums) {
            xorRes ^= x;
        }
        int temp = 1; // 用来标志第几位是 1
        while (true) {
            if ((xorRes & 1) == 1) {
                break;
            }
            temp = temp << 1;
            xorRes = xorRes >> 1; // 右移，从低到高
        }

        for (int y : nums) {
            if ((y & temp) == 0) { // 对应位是 0
                res[0] ^= y;
            } else {
                res[1] ^= y;
            }
        }
        return res;
    }
}
```

<font size = 5>**Peace!**

