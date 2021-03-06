# 剑指 Offer 50. 第一个只出现一次的字符

> https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/

## 1. 问题描述

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

示例:

s = "abaccdeff"
返回 "b"

s = "" 
返回 " "
 

限制：

0 <= s 的长度 <= 50000

## 2. 思路

使用hash表记录每个字符出现的次数

```cpp
class Solution {
public:
    char firstUniqChar(string s) {
        unordered_map<char, int> hash;
        // hash记录每个字符出现的次数
        for(auto c : s){
            if(hash.count(c) > 0) ++hash[c];
            else hash[c] = 1;
        }
        // 当次数为1则输出
        for(auto c : s){
            if(hash[c] == 1) return c;
        }
        return ' ';
    }
};
```