[Problem Statement](https://leetcode.com/problems/reverse-linked-list/)

## Approach :- In this approach, we'll iterating the list with tracking of previous node ,current node and next pointer.
Initializations - 
- Assign previous as head
- Assign current as head->next
- Assing head->next to null because finally its going to become our tail node.

Now until current->next is not null
- next = curr->next
- curr->next = previous
- previous = curr

After termination of loop
- curr->next = previous
return curr.

```cpp
// Time Complexity - O(N)             Space Complexity - O(1)
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (head == NULL)
            return NULL;
        if (head->next == NULL)
            return head;
        // Previous pointer
        ListNode *previous = head;
        // Current pointer
        ListNode *curr = head->next;
        head->next = NULL;
        while (curr->next) {
            ListNode *next = curr->next;
            curr->next = previous;
            previous = curr;
            curr = next;
        }
        curr->next = previous;
        return curr;
    }
};
```
