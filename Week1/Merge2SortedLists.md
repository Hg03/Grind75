[Problem Statement](https://leetcode.com/problems/merge-two-sorted-lists)

## Approach 1 :- In this approach, we'll check the nodes' correspondingly and assign the sorted list in node's(which has lesser value) next. 

```cpp
// Time Complexity(as well as space) - O(m + n) where m and n is the length of the linked list
class Solution {
public:
    ListNode* merge(ListNode* list1, ListNode* list2)
    {
        if(list1 == NULL) return list2;
        if(list2 == NULL) return list1;
        if(list1->val < list2->val)
        {
            list1->next = merge(list1->next,list2);
            return list1;
        }
        else
        {
            list2->next = merge(list1,list2->next);
            return list2;
        }
        
    }
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        return merge(list1,list2);
    }
};
```

## Approach 2 :- In this approach, we'll create a dummy list, then the two list given correspondingly node by node and check the value's lesserness.

```cpp
// Time Complexity - O(m+n)         Space Complexity - O(1)
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if(list1 == NULL) return list2;
        if(list2 == NULL) return list1;
        ListNode *ans, *tail;
        // Decide head for the resulted linked list
        if(list1->val < list2->val)
        {
            ans = list1;
            tail = list1;
            list1 = list1->next;
        }
        else
        {
            ans = list2;
            tail = list2;
            list2 = list2->next;
        }
        
        // Traverse further
        while(list1 && list2)
        {
            if(list1->val < list2->val)
            {
                tail->next = list1;
                tail = list1;
                list1 = list1->next;
            }
            else
            {
                tail->next = list2;
                tail = list2;
                list2 = list2->next;
            }
        }
        
        // Merging remaining linked list
        if(!list1) tail->next = list2;
        else tail->next = list1;
        
        return ans;
    }
};
```
