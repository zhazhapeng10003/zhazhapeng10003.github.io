---
title: 剑指Offer（三十）：连续子数组的最大和（dp）
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
abbrlink: 37315
date: 2020-04-02 00:15:44
coverImg:
tags:
  - 剑指Offer
  - 数组
categories: 刷题
password:
---

## 连续子数组的最大和:
#### 题目链接：
[牛客网](//www.nowcoder.com/practice/459bd355da1549fa8a49e350bf3df484?tpId=13&tqId=11183&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是1)<br/>
**<font size = 3>示例 1：**
>**输入:** nums = [-2,1,-3,4,-1,2,1,-5,4]
**输出:** 6
**解释:** 连续子数组 [4,-1,2,1] 的和最大，为 6
#### 解题思路：<br/>
此题可以用动态规划来达到最优解，如下：

**<font size = 3>•** **状态定义：** 设动态规划列表 dpdp ，dp[i] 代表以元素 nums[i] 为结尾的连续子数组最大和。<br/>
**<font size = 3>•** **转移方程：** 若 *dp*[i - 1] ≤ 0 ，说明 *dp*[i - 1]  对 *dp*[ i ]  产生负贡献，即 *dp*[i - 1]  + *nums*[ i ] 还不如 *nums*[ i ] 本身大。
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** 当 *dp*[i - 1] > 0 时：执行 *dp*[ i ] = *dp*[i - 1] + nums*[ i ]；
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** 当 *dp*[i - 1] ≤ 0 时：执行 *dp*[ i ] = *nums*[ i ]；<br/>
**<font size = 3>•** **初始状态：** *dp*[ 0 ] = *nums*[ 0 ] ，即以 *nums*[ 0 ] 结尾的连续子数组最大和为 *nums*[ 0 ] 。<br/>
**<font size = 3>•** **返回值：** 返回 *dp* 列表中的最大值，代表全局最大值。
<center>
<img src="https://img-blog.csdnimg.cn/20200323123726174.png" width="50%"> <br/>
</center>

#### 复杂度：<br/>
时间复杂度： ***O*(N)**， 线性遍历数组 numsnums 即可获得结果，使用 *O*(N) 时间。
空间复杂度：***O*(1)**，使用常数大小的额外空间。
#### 代码实现：<br/>
```java
public class Solution {
    public static int FindGreatestSumOfSubArray(int[] array){
        if (array == null || array.length == 0) {
            return 0;
        }

        int n = array.length;
        int[] dp = new  int[n];
        dp[0] = array[0];
        int result = dp[0];
        for (int i = 1; i < n; ++i){
            dp[i] = Math.max(dp[i-1], 0) + array[i];
            result = Math.max(result, dp[i]);
        }
        return result;
    }
}
```
**<font size = 3>•** **空间复杂度降低：**
&ensp;&ensp;&ensp;&ensp;由于 *dp*[ i ] 只与 *dp*[i - 1]  和 *nums*[ i ] 有关系，因此可以将原数组 *nums* 用作 *dp* 列表，即直接在 *nums* 上修改即可。
由于省去 *dp* 列表使用的额外空间，因此空间复杂度从 ***O*(N)** 降至 ***O*(1)**。
#### 代码实现：<br/>

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        for(int i = 1; i < nums.length; i++) {
            nums[i] += Math.max(nums[i - 1], 0);
            res = Math.max(res, nums[i]);
        }
        return res;
    }
}
```

<font size = 5>**Peace!**
