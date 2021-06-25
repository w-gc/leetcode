# 剑指 Offer 55 - I. 二叉树的深度

> https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/

## 1.问题描述

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

例如：

给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。

 

提示：

节点总数 <= 10000
注意：本题与主站 104 题相同：https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/

## 2.思路

递归+max

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
};
```

深度优先

```cpp
class Solution {
public:
    void dfs(TreeNode* root, int depth, int &max_depth){
        if(root == nullptr){
            max_depth = max(depth, max_depth);
            return;
        } 
        dfs(root->left, depth + 1, max_depth);
        dfs(root->right, depth + 1, max_depth);
    }

    int maxDepth(TreeNode* root) {
        int max_depth = 0;
        dfs(root, 0, max_depth);
        return max_depth;
    }
};
```


广度优先（层序遍历）

```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == nullptr) return 0;
        int res = 0;
        queue<TreeNode*> Q;
        Q.push(root);
        while(!Q.empty()){
            int size = Q.size(); // 记录当前层的长度
            while(size-- > 0){
                TreeNode* p = Q.front();
                Q.pop();
                if(p->left != nullptr) Q.push(p->left);
                if(p->right != nullptr) Q.push(p->right);
            }
            ++res;
        }
        return res;
    }
};
```