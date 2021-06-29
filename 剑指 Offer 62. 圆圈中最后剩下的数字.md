# 剑指 Offer 62. 圆圈中最后剩下的数字

## 1. 问题描述

0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。

 

示例 1：

输入: n = 5, m = 3
输出: 3
示例 2：

输入: n = 10, m = 17
输出: 2
 

限制：

1 <= n <= 10^5
1 <= m <= 10^6
通过次数90,526提交次数138,430

## 2. 思路

- 模拟法

```cpp
// 超时
class Solution {
public:
    int lastRemaining(int n, int m) {
        vector<bool> visited(n, false); // 记录是否访问过
        int i = 0, j = 0;
        int cnt = 0;                    // 记录删除元素的数量
        while(cnt < n - 1){
            if(visited[i] == false) ++j;
            if(j == m){
                j = 0;                  // 从0开始数，数到m就删除
                visited[i] = true;
                ++cnt;
            }
            i = (i + 1) % n;
        }
        i = 0;
        while( visited[i] ) ++i;        // 找出最后一个未删除的
        return i;
    }
};
```

- 递归处理

如 n = 5, m = 3, 则最后的时3

那么 n = 6, m = 3, 则在 0, 1, 2, 3, 4, 5 中，先删除2，得 0, 1, 3, 4, 5

重排后为 3(0), 4(1), 5(2), 0(3), 1(4). 根据n=5, m=3得到为 0(3)

```cpp
class Solution {
public:
    int lastRemaining(int n, int m) {
        if(n == 1) return 0;
        int x = lastRemaining(n - 1, m);
        return (m + x) % n;
    }
};
```

- 迭代法

将递归展开

```cpp
class Solution {
public:
    int lastRemaining(int n, int m) {
        int res = 0;
        for(int i = 1; i <= n; ++i)
            res = (res + m) % i;
        return res;
    }
};
```