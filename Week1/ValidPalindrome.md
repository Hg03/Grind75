[Problem Statement](https://leetcode.com/problems/valid-palindrome)

## Approach :- In this approach, we'll use two pointer in which left is at beginning and right is at the end. Then we'll iterate through string and check if string of left and string of right is equal or not with keeping in mind that we'll ignore the spaces by incrementing left or decrementing right.

```cpp
// Time Complexity - O(logn)              Space Complexity - O(1)
class Solution {
public:
    bool isPalindrome(string s) {
        int size = s.size();
        int left = 0,right = size-1;
        while(left < right)
        {
            if(!isalnum(s[left])) left++;
            else if(!isalnum(s[right])) right--;
            else if(tolower(s[left])!=tolower(s[right])) return false;
            else
            {
                left++;
                right--;
            }
        }
        return true;
    }
};
```

