[Problem Statement](https://leetcode.com/problems/coin-change/)


## Approach 1 [Recursive] :- In this approach, we'll iterate with each coins and check for remaining amount required.

```cpp
// Time Complexity - O(amount^n)        Space Complexity - O(n)
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

## Approach 2 [DP] :- In this approach, create an array of size amount(given) and keep all value to amount+! initially and then make first to be 0. Now check for each indices , like at 1st indices, we see how many ways we can choose the coins to make amount equal to 1, then to 2(at 2 no. indices), then to 3 and so on to last of amount.

```cpp
// Time Complexity - O(amount*coins.size())             Space Complexity - O(amount.size())
class Solution
{
public:
     int coinChange(vector<int> &coins, int amount)
     {
         vector<int> dp(amount+1,amount+1);
         dp[0] = 0;
         
         for(int coin : coins)
         {
             for(int i=coin;i<=amount;i++)
             {
                 dp[i] = min(dp[i],dp[i-coin]+1);
             }
         }
         return dp[amount] <= amount ? dp[amount] : -1;
     }
};
```
