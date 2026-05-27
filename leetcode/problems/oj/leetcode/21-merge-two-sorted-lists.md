#链表 
[21. 合并两个有序链表 - 力扣（LeetCode）](https://leetcode.cn/problems/merge-two-sorted-lists/)
>gpt辅助
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode list3 = ListNode();
        ListNode * p3 = &list3;
        while(list1 && list2){
            if(list1->val < list2->val){
                p3->next=list1;
                list1=list1->next; 
            }
            else{
                p3->next=list2;
                list2=list2->next; 
            }
            p3=p3->next;
        }
        p3->next = list1?list1:list2;
        return list3.next;
    }
};
```