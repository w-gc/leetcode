# 剑指 Offer 24. 反转链表

> https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/

## 1. 问题描述

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

 

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
 

限制：

0 <= 节点个数 <= 5000

## 2. 思路

每次从将旧链表中的头结点插入到新链表中

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head == nullptr) return nullptr;     // 边界情况
        ListNode* newHead = nullptr;
        ListNode* p = head->next;
        
        while(head != nullptr){
            head->next = newHead;               // 将旧链表的头结点插入到新链表
            newHead = head;                     // 更新新链表的头指针
            head = p;                           // 更新旧链表的头指针（删除了一结点）
            if(p != nullptr) p = p->next;       // 指向旧链表的第二结点的指针往后挪
        }
        return newHead;
    }
};
```