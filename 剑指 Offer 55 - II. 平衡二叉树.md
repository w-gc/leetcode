# 剑指 Offer 55 - II. 平衡二叉树

>

## 1.问题描述

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

 

示例 1:

给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
返回 true 。

示例 2:

给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。

 

限制：

0 <= 树的结点个数 <= 10000
注意：本题与主站 110 题相同：https://leetcode-cn.com/problems/balanced-binary-tree/


## 2.思路

利用条件：

- 左右子树的高度差不超过1
- 左右子树也是平衡的
 
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == nullptr) return 0;
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
    bool isBalanced(TreeNode* root) {
        if(root == nullptr) return true;
        return abs(maxDepth(root->left) - maxDepth(root->right)) < 2 && isBalanced(root->left) && isBalanced(root->right);
    }
};
```
自顶向下，冗余多，求深度从顶到下，递归处理左右子树又得从顶到下

自下向顶，就是在求深度的时候，顺便做判断，添加`-1`做状态

```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == nullptr) return 0;

        // 如果左右子树出现-1，剪枝，终止
        int maxleft = maxDepth(root->left);
        if(maxleft == -1) return -1;

        int maxright = maxDepth(root->right);
        if(maxright == -1) return -1;

        // 高度差不超过1则正常返回高度
        // 超过1，则返回状态-1
        return abs(maxleft - maxright) < 2 ? max(maxleft, maxright) + 1 : - 1;
    }
    bool isBalanced(TreeNode* root) {
        return maxDepth(root) != -1;
    }
};
```