---
title: 剑指Offer（十九）：顺时针打印矩阵
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
abbrlink: 54653
date: 2020-04-01 23:51:46
coverImg:
tags:
  - 剑指Offer
  - 数组
categories: 刷题
password:
---


## 顺时针打印矩阵:
#### 题目链接：
[牛客网](//www.nowcoder.com/practice/9b4c81a02cd34f76be2659fa0d54342a?tpId=13&tqId=11172&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。<br/>
**示例 1：**
>**输入:** matrix = [&ensp;[1,2,3],
>	&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;[4,5,6],
>&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;[7,8,9]&ensp;]  
**输出:** [1,2,3,6,9,8,7,4,5]

**示例 2：**
>**输入:** matrix = [&ensp;[1,2,3,4],
>&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;[5,6,7,8],
>&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;[9,10,11,12]&ensp;]
**输出:** [1,2,3,4,8,12,11,10,9,5,6,7]

#### 解题思路：<br/>
模拟法（模拟矩阵打印的顺时针走）：用四个标志位置就可以进行解决（代码中的low、high、left、right代表了即将访问的上下左右四条线）。
#### 复杂度：<br/>
时间复杂度 *O*(*M N*) ： M, N 分别为矩阵行数和列数。
空间复杂度 *O*(1) ： 四个边界 **l** , **r** , **t** , **b** 使用常数大小的 **额外** 空间（ <font color = red>res<font color = black> 为必须使用的空间）


#### 代码实现：<br/>
```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> printMatrix(int [][] matrix) {
        if(matrix==null)
            return null;
        ArrayList<Integer> list=new ArrayList<Integer> ();
        int row=matrix.length;
        int col=matrix[0].length;
        int left=0,top=0,right=col-1,bottom=row-1;
        while(left<=right&&top<=bottom){
            //从左向右
            for(int i=left;i<=right;i++){
                list.add(matrix[top][i]);
            }
            //从上到下（从下一行开始向下走）
            for(int j=top+1;j<=bottom;j++){
                list.add(matrix[j][right]);
            }
            //从右到左
            if(top!=bottom){
                for(int k=right-1;k>=left;k--){
                    list.add(matrix[bottom][k]);
                }
            }
            //从下到上
            if(left!=right){
                for(int l=bottom-1;l>top;l--){
                    list.add(matrix[l][left]);
                }
            }

            //下一个正方形矩阵
            top++;left++;right--;bottom--;
        }
        return list;
    }
}
```
<font size = 5>**Peace!**
