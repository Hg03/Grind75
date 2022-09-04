[Problem Statement](https://leetcode.com/problems/partition-equal-subset-sum)

## Approach 1 [Recursive] :- In this approach, we'll calculate the whole array sum, if it is odd then return false otherwise calculate the half of sum, then use the function subset sum upto k and check the half sum, if it founds return true.


## Approach 2 [Dynamic Programming] :- 

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for(int i:nums)
        {
            sum+=i;
        }
        if(sum%2!=0) return false;
        
        sum = sum/2;
        vector<bool> dp(sum+1);
        dp[0] = true;
        for(int i:nums)
        {
            for(int j=sum;j>=i;j--)
            {
                dp[j] = dp[j] | dp[j-i];
            }
        }
        return dp[sum];
    }
};
```
