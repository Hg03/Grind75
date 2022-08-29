[Problem Statement](https://leetcode.com/problems/string-to-integer-atoi)

## Approach :- We'll just iterate the string and checks the whitespaces, character and signs using some conditions.

```cpp
// Time Complexity - O()
class Solution {
public:
	int myAtoi(string s) {
        if(s.length() == 0) return 0;
	int i = 0;
	int n = s.size();
	while (i < n && (s[i] == ' ')) i++;  // If whitespaces occurs, just go forward
        s = s.substr(i); // Filter the left out string without whitespace in beginning
        int sign = 1;    // Checking for positve/negative sign
        if(s[0] == '-') sign = -1;   // If beginning of string is '-' sign is negative
        
        
        i = (s[0] =='-' || s[0] =='+')? 1 : 0;  // If is there any sign at begining, we should start with next of it
        
	long num = 0;
	while (i < n) {
            if(s[0] == ' ' || !isdigit(s[i])) break;  // If now we encounter any whitespace or non digit, it is not a digit
            
			num = num * 10 + (s[i] - '0');          // Substracting '0' from character, results integer format
            if(sign == 1 && num > INT_MAX) return INT_MAX;     // Checking is number is greater than int max ?
            if(sign == -1 && -1 * num < INT_MIN) return INT_MIN;   // Checking is number is lesser than int min ?
	    i++;
	}
	return sign * num;
}
};
```
