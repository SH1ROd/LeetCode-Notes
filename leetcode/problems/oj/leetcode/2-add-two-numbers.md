[2. 两数相加 - 力扣（LeetCode）](https://leetcode.cn/problems/add-two-numbers/)

>溢出
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
 */class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        long long a = l1->val;
        long long n = 10;
        while(l1->next!=NULL){
            l1 = l1->next;
            a = a + l1->val * n;
            n = n * 10;
        }
        long long b = l2->val;
        n = 10;
        while(l2->next!=NULL){
            l2 = l2->next;
            b = b + l2->val * n;
            n*=10;
        }
        long long ans = a + b;
        cout << a << " " << b << endl;
        cout << ans  << endl;
        ListNode* head = new ListNode;
        head->next = nullptr;
        ListNode* now = head;
        if (ans==0){
            head->val = 0;
            return head;
        }
        while(ans > 0){
            int x = ans % 10;
            ListNode* temp = temp;
            temp = new ListNode;
            temp->next = nullptr;
            temp->val = x;
            now->next = temp;
            now = now->next;
            ans/=10;
        }
        return head->next;
    }
};
```

>通过(一位一位加)
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
 */class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        vector<int> a;
        while(l1!=NULL){
            a.push_back(l1->val);
            l1 = l1->next;
        }
        vector<int> b;
        while(l2!=NULL){
            b.push_back(l2->val);
            l2 = l2->next;
        }
        int n = max(a.size(), b.size());
        a.resize(n);
        b.resize(n);
        ListNode* head = new ListNode;
        head->next = nullptr;
        ListNode* now = head;
        int i = 0;
        int c = 0;
        while(i < n || c > 0){
            int sum = c;
            if(i < n){
                sum += a[i] + b[i];
            }
            int x = sum % 10;
            c = sum / 10;
            ListNode* temp = temp;
            temp = new ListNode;
            temp->next = nullptr;
            temp->val = x;
            now->next = temp;
            now = now->next;
            i++;
        }
        return head->next;
    }
};
```

>缩短
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        vector<int> a;
        while(l1!=NULL){
            a.push_back(l1->val);
            l1 = l1->next;
        }
        vector<int> b;
        while(l2!=NULL){
            b.push_back(l2->val);
            l2 = l2->next;
        }
        int n = max(a.size(), b.size());
        a.resize(n);
        b.resize(n);
        ListNode* head = new ListNode();
        ListNode* now = head;
        int i = 0;
        int c = 0;
        while(i < n || c > 0){
            int sum = c;
            if(i < n){
                sum += a[i] + b[i];
            }
            int x = sum % 10;
            c = sum / 10;
            ListNode* temp = new ListNode(x);
            now->next = temp;
            now = now->next;
            i++;
        }
        return head->next;
    }
};
```

>宜均版本
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:

        num1 = 0
        num2 = 0
        multiplier = 1
        current1 = l1
        current2 = l2
        
        while current1:
            num1 += current1.val * multiplier
            current1 = current1.next
            multiplier *= 10
            
        multiplier = 1
        
        while current2:
            num2 += current2.val * multiplier
            current2 = current2.next
            multiplier *= 10
            
        total = num1 + num2
        
        if total == 0:
            return ListNode(0)
            
        head = None
        prev = None
        
        while total > 0:
            digit = total % 10
            node = ListNode(digit)
            
            if head == None:
                head = node
                prev = head
            else:
                prev.next = node
                prev = prev.next
                
            total //= 10
            
        return head
```

>GPT
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = ListNode(0)  # dummy 節點方便返回
        current = dummy
        carry = 0
        
        while l1 or l2 or carry:
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0
            
            total = val1 + val2 + carry
            carry, digit = divmod(total, 10)  # digit 放節點，carry 下一輪進位
            
            current.next = ListNode(digit)
            current = current.next
            
            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next
                
        return dummy.next
```

### ✅ 正确方式

记 **3个关键点就够了**：

1. **同时遍历两个链表**
    
2. **carry 参与计算**
    
3. **每一步新建节点**

>下一版

```python

```