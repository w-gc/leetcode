# 剑指 Offer 32 - III. 从上到下打印二叉树 III

> https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/

## 1.问题描述

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [20,9],
  [15,7]
]
 

提示：

节点总数 <= 1000

## 2.思路

层数遍历，偶数层翻转存储

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        if(root == nullptr) return {};
        vector<vector<int>> res;
        bool left2right = true;
        queue<TreeNode*> Q;
        Q.push(root);
        while(!Q.empty()){
            int size = Q.size();
            vector<int> tmp;
            while(size > 0){
                TreeNode* p = Q.front();
                Q.pop();
                tmp.push_back(p->val);
                if(p->left != nullptr) Q.push(p->left);
                if(p->right != nullptr) Q.push(p->right);
                --size;
            }
            if(!left2right) reverse(tmp.begin(), tmp.end());
            res.push_back(tmp);
            left2right = !left2right;
        }
        return res;
    }
};
```

使用双向队列，在遍历元素的时候就区分左右两个方向

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        if(root == nullptr) return {};
        vector<vector<int>> res;

        bool left2right = true;
        TreeNode *p = nullptr;

        deque<TreeNode*> Q;
        Q.push_back(root);

        while(!Q.empty()){
            vector<int> tmp;
            int size = Q.size();
            while(size > 0){
                if(left2right){ // 从左到右，和用队列的一致
                    p = Q.front();
                    Q.pop_front();
                    if(p->left != nullptr) Q.push_back(p->left);
                    if(p->right != nullptr) Q.push_back(p->right);
                } else {
                    // 方向相反，出队列和进队列的顺序
                    p = Q.back();
                    Q.pop_back();
                    // 特别注意，左右子树的顺序相反
                    if(p->right != nullptr) Q.push_front(p->right);
                    if(p->left != nullptr) Q.push_front(p->left);
                }
                tmp.push_back(p->val);
                --size;
            }
            res.push_back(tmp);
            left2right = !left2right;
        }
        return res;
    }
};
```