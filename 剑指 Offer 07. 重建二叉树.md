# 剑指 Offer 07. 重建二叉树

>

## 1. 问题描述

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

 

例如，给出

前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
 

限制：

0 <= 节点个数 <= 5000

 

注意：本题与主站 105 题重复：https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/


## 2. 思路

递归处理

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
    TreeNode* buildTree(vector<int> preorder, vector<int> inorder) {
        if(preorder.empty()) return nullptr;
        TreeNode *root = new TreeNode(preorder[0]);
        int idx = 0;
        while(inorder[idx] != root->val) ++idx;
        root->left = buildTree({preorder.begin() + 1, preorder.begin() + 1 + idx}, {inorder.begin(), inorder.begin() + idx});
        root->right = buildTree({preorder.begin() + 1 + idx, preorder.end()}, {inorder.begin() + idx + 1, inorder.end()});
        return root;
    }
};
```