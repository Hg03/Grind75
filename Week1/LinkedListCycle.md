[Problem Statement](https://leetcode.com/problems/linked-list-cycle/)

## Approach 1 :- In this approach, we'll create a hashset which stores node. Then we traverse the linked list and store the node one by one and check that isn't that node is preexist in that set, if yes return true.

```cpp
// Time Complexity - O(n)           Space Complexity - O(n)
class Solution {
public:
    bool hasCycle(ListNode *head) {
         unordered_set<ListNode*> s;
         while(head!=NULL)
         {
             if(s.find(head) != s.end()) return true;
             s.insert(head);
             head = head->next;
         }
         return false;
    }
};
```

## Approach 2 :- In this approach, we'll use slow and fast pointer(slow pointer move by one node and fast by two), so traverse the last using slow and fast pointer and if slow is equal to fast ,we'll return true else false.

```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
          ListNode* slow = head;
          ListNode* fast = head;
          while(fast != NULL && fast->next != NULL)
          {
              slow = slow->next;
              fast = fast->next->next;
              if(slow == fast) return true;
          }
          return false;
    }
};
```
