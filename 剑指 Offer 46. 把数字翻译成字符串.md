# 剑指 Offer 46. 把数字翻译成字符串

> https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/

## 1. 问题描述

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

示例 1:

输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
 

提示：

0 <= num < 231

## 2. 思路

深度优先（递归）

```cpp
class Solution {
public:
    int translateNum(int num) {
        if(num == 0) return 1;  // 终止条件
        else if( num % 100 < 26 && num % 100 >= 10){
            // 10~25 有两种情况，分别递归处理
            return translateNum(num / 100) + translateNum(num / 10);
        }else{
            // 0 ~ 9 只有一种情况，继续递归
            return translateNum(num / 10);
        }
    }
};
```

使用动态规划，已`dp[i]`表示已`i`结尾的部分中能翻译方法的数量。
那么
$$
dp[i] = \begin{cases}
    dp[i - 1] + dp[i - 2] & 10 \leq 10 * num[i-1] + num[i] \leq 25 \\
    dp[i - 1] & \text{otherwise}
\end{cases}
$$

```cpp
class Solution {
public:
    int translateNum(int num) {
        string str = to_string(num);
        int dp_1 = 1, dp_2 = 1; // 分别是dp[i-1]和dp[i-2]
        for(int i = 2, len = str.size(); i <= len; ++i){
            string tmp = str.substr(i - 2, 2);
            // 状态转移
            int dp = tmp >= "10" && tmp <= "25" ? dp_1 + dp_2 : dp_1;
            dp_2 = dp_1;
            dp_1 = dp;
        }
        return dp_1;
    }
};
```