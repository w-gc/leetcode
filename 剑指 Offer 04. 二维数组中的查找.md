# 剑指 Offer 04. 二维数组中的查找

> https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/

## 1. 问题描述

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

示例:

现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。

 

限制：

0 <= n <= 1000

0 <= m <= 1000

 

注意：本题与主站 240 题相同：https://leetcode-cn.com/problems/search-a-2d-matrix-ii/

## 2. 思路描述

有序，必二分。

从左下角 Matrix[nrows - 1][0] 出发，如果比target大，则往上一行，小则下一列。

```cpp
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if(matrix.empty()) return false;
        int ncols = matrix[0].size();
        int row =  matrix.size() - 1;
        int col = 0;
        while (row >= 0 && col < ncols){
            if(matrix[row][col] == target) return true;
            else if(matrix[row][col] > target) --row;
            else ++col;
        }
        return false;
    }
};
```