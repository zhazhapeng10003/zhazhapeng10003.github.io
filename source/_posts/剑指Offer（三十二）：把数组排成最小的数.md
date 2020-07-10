---
title: 剑指Offer（三十二）：把数组排成最小的数
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/4.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
abbrlink: 56735
date: 2020-04-02 00:18:16
coverImg:
tags:
  - 剑指Offer
  - 数组
categories: 刷题
password:
---


## 把数组排成最小的数:
#### 题目链接：
[牛客网](//www.nowcoder.com/practice/9f3231a991af4f55b95579b44b7a01ba?tpId=13&tqId=11159&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)<br>
#### 题目描述：
&ensp;&ensp;&ensp;&ensp;输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。<br/>
**<font size = 3>示例 1：**
>**输入:** [10,2]
**输出:** "102"

**<font size = 3>示例 2：**
>**输入:** [3,30,34,5,9]
**输出:** "3033459"
#### 解题思路：<br/>
&ensp;&ensp;&ensp;&ensp;比较两个字符串 s1, s2 大小的时候，先将它们拼接起来，比较 s1+s2 ,和 s2+s1 那个大，如果 s1+s2 大，那说明 s2 应该放前面，所以按这个规则，s2 就应该排在 s1 前面。
#### 代码实现：<br/>
**<font size = 3>•** 第一种（耗时最长 42ms，自己编写的比较方法，两个for循环），并且int有大小限制，可替换成long型：
```java
import java.util.ArrayList;
public class Solution {
    public String PrintMinNumber(int [] numbers) {
        if (numbers == null || numbers.length == 0){
            return "";
        }
        for (int i = 0; i < numbers.length; ++i){
            for (int j = i + 1; j < numbers.length; ++j){
                int num1 = Integer.valueOf(numbers[i] + "" + numbers[j]);
                //long num1 = Long.valueOf(numbers[i] + "" + numbers[j]);
                int num2 = Integer.valueOf(numbers[j] + "" + numbers[i]);
                //long num2 = Long.valueOf(numbers[j] + "" + numbers[i]);
                if (num1 > num2){
                    int temp = numbers[j];
                    numbers[j] = numbers[i];
                    numbers[i] = temp;
                }
            }
        }
        StringBuilder ans = new StringBuilder();
        for (int i : numbers){
            ans.append(i);
        }
        return ans.toString();
    }
}
```
**<font size = 3>•** 第二种（自定义排序规则 String[ ] ，耗时最短 **6ms**）：

```java
class Solution {
    public String minNumber(int[] nums) {
        String[] strNumbers = new String[nums.length];
        for (int i = 0; i < nums.length; ++i){
            strNumbers[i] = String.valueOf(nums[i]);
        }
        //排序（传入一个比较器对象）
        Arrays.sort(strNumbers, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return (o1 + o2).compareTo(o2 + o1);//升序
            }
        });
        //元素拼接
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < strNumbers.length; ++i){
            sb.append(strNumbers[i]);
        }
        return sb.toString();
    }
}
```
**<font size = 3>•** 第三种（自定义排序规则 ArrayList< String > ，耗时比第二种稍长，9ms）：
```java
import java.util.ArrayList;
class Solution {
    public String minNumber(int[] nums) {
        ArrayList<String> strList = new ArrayList<>();
        for (int num : nums) {
            strList.add(String.valueOf(num));
        }
        strList.sort((s1, s2) -> (s1 + s2).compareTo(s2 + s1));
        StringBuilder sb = new StringBuilder();
        for (String str : strList) {
            sb.append(str);
        }
        return sb.toString();
    }
}
```
<font size = 5>**Peace!**
