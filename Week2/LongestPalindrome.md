[Problem Statement](https://leetcode.com/problems/longest-palindrome/submissions/)

## Approach :- Simple approach is based on the occurences of character in string. 
- If character count is even, then its each occurences is utilized in forming the palindrome. (means even count can be partnered. One on left and another on right)
- If character count is odd, then its occurences -1 can be utilized. (if 5 (for example) ,4 can be partnered, one is utilized in middle)

```cpp
// Time Complexity - O(N)            Space Complexity - O(1)
class Solution {
public:
    int longestPalindrome(string s) {
        int occurences[128] = {0};
        int len = 0;
        for(char letter : s) occurences[(int)letter]++;
        for(int occu : occurences)
        {
            if(occu%2==0)
                len+=occu;
            else len+=(occu-1);
        }
        if(len < s.size()) len++;
        return len;
    }
};
```
