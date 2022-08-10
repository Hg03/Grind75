[Problem Statement](https://leetcode.com/problems/middle-of-the-linked-list/)

## Approach 1 :- In this approach, we'll iterate the whole list once using while and calcuate its length. Now we divide our length by 2 and iterate the list again upto half(length updated).

```cpp
// Time Complexity - O(n)          Space Complexity - O(1)
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
    ListNode* middleNode(ListNode* head) {
        int length = 1;
        int i=1;
        ListNode* temp = head;
        while(temp->next!=NULL)
        {
            temp = temp->next;
            length++;
        }
        length = length/2;

        temp = head;
        while(i<=length)
        {
            temp = temp->next;
            i++;
            
        }
        return temp;
    }
};
```

## Approach 2 :- In this approach, we'll use slow and fast pointer in which slow move by 1 and fast move by 2. Iterate the list using slow and fast until fast or fast->next is not null. After termination of loop, return slow pointer.

```cpp
// Time Complexity - O(n)           Space Complexity - O(1)
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast!=NULL && fast->next != NULL)
        {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
};
```
