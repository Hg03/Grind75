[Problem Statement](https://leetcode.com/add-binary/)

## Approach 1 :- In this approach, we'll iterate both strings and calculate the sum and keep track of carry and one by one assigning it into result.

```cpp
// Time Complexity - O(n)           Space Complexity - O(n)
class Solution {
 public:
  string addBinary(string a, string b) {
    string ans;
    int carry = 0;
    int i = a.length() - 1;
    int j = b.length() - 1;

    while (i >= 0 || j >= 0 || carry) {
      if (i >= 0)
        carry += a[i--] - '0';
      if (j >= 0)
        carry += b[j--] - '0';
      ans += carry % 2 + '0';
      carry /= 2;
    }

    reverse(begin(ans), end(ans));
    return ans;
  }
};
```
