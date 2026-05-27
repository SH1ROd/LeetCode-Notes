#链表 #双指针
[LCR 171. 训练计划 V - 力扣（LeetCode）](https://leetcode.cn/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/description/)

> 我的题解
```c++
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(headA==NULL || headB==NULL){
            return NULL;
        }
        ListNode *a = headA;
        ListNode *b = headB;
        while(a!=b){
            if(a->next==NULL && b->next==NULL){
                return a->next;
            }
            if(a->next==NULL){
                a = headB;
            }
            else{
                a=a->next;
            }
            if(b->next==NULL){
                b = headA;
            }
            else{
                b=b->next;
            }
        }
        return a;
    }
};
```

>我的略微改进
```c++
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(headA==NULL || headB==NULL){
            return NULL;
        }
        ListNode *a = headA;
        ListNode *b = headB;
        while(a!=b){
            if(a==NULL){
                a = headB;
            }
            else{
                a=a->next;
            }
            if(b==NULL){
                b = headA;
            }
            else{
                b=b->next;
            }
        }
        return a;
    }
};
```

>gpt
```c++
class Solution {
public:
    ListNode* FindFirstCommonNode(ListNode* pHead1, ListNode* pHead2) {
        if (!pHead1 || !pHead2) return nullptr;

        ListNode *p1 = pHead1, *p2 = pHead2;

        while (p1 != p2) {
            p1 = p1 ? p1->next : pHead2;
            p2 = p2 ? p2->next : pHead1;
        }

        return p1;
    }
};

```