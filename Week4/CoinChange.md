[Problem Statement](https://leetcode.com/problems/coin-change/)


## Approach 1 [Recursive] :- In this approach, we'll iterate with each coins and check for remaining amount required.

```cpp
class Solution
{
public:
     int count(int amount, vector<int> &coins, int n, int i)
     {
          if (amount == 0)  // If amount is equal to zero, we don't need more coins so return 0
          {
               return 0;
          }
          if (i == n)     // If we reach to an end
          {
               return INT_MAX - 1;
          }
          int res = -1;
          int reject = count(amount, coins, n, i + 1);  
          res = reject;

          int accept = 0;
          if (amount >= coins[i])
          {
               accept = 1 + count(amount - coins[i], coins, n, i);
               res = min(res, accept);
          }
          
          return res;
     }

     int coinChange(vector<int> &coins, int amount)
     {
          int n = coins.size();
          int res = count(amount, coins, n, 0);
          return res == INT_MAX - 1 ? -1 : res;
     }
};
```
