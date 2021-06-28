# 剑指 Offer 05. 替换空格

> https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/

## 1. 问题描述

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

示例 1：

输入：s = "We are happy."
输出："We%20are%20happy."
 

限制：

0 <= s 的长度 <= 10000

## 2. 思路

使用`string`自带的find和replace方法

```cpp
class Solution {
public:
    string replaceSpace(string s) {
        auto t = s.find(' ');
        while(t != string::npos){
            s.replace(t, 1, "%20");
            t = s.find(' ');
        }
        return s;
    }
};
```