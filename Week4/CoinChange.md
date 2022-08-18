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

## Approach 2 [DP] :- In this approach, create an array of size amount(given) and keep all value to INT_MAX initially and then make first to be 0.

```cpp
// Time Complexity - O(amount*coins.size())             Space Complexity - O(amount.size())
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        // Initialize DP array with INT_MAX and dp[0]=0
        int dp[amount+1];
        dp[0]=0;
        for(int i=1;i<=amount;++i)
            dp[i] = INT_MAX;

        int len = coins.size();

        // Fill DP array from amount=1 to amount's actual value
        for (int i = 1; i <= amount; ++i)
        {
            // Try to include all the coins one by one
            for (int j = 0; j < len; ++j)
            {
                // If this coin is usable(value less than current amount)
                if(coins[j] <= i){
                    // What is the cost for rest of the amount
                    // If I use this coin
                    // eg. if amount=8 and coins[j]=5 then rest is min cost
                    // for 8-5 = 3
                    int rest = dp[i-coins[j]];
                    // If including this coin gives lesser value 
                    // than current min value then include it
                    if(rest != INT_MAX && rest+1<dp[i]){
                        // update min value for amount=i
                        dp[i] = rest+1;
                    }
                }
            }
        }
        return dp[amount]==INT_MAX ? -1 : dp[amount];
    }
};
```
