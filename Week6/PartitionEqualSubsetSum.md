[Problem Statement](https://leetcode.com/problems/partition-equal-subset-sum)

## Approach 1 [Recursive] :- In this approach, we'll calculate the whole array sum, if it is odd then return false otherwise calculate the half of sum, then use the function subset sum equal to target and check the half sum, if it founds return true.

```cpp
class Solution {
public:
    bool subsetSumUtil(int ind, int target, vector<int>& arr, vector<vector<int>> &dp)
    {
        if(target==0)
            return true;

        if(ind == 0)
            return arr[0] == target;

        if(dp[ind][target]!=-1)
            return dp[ind][target];

        bool notTaken = subsetSumUtil(ind-1,target,arr,dp);

        bool taken = false;
        if(arr[ind]<=target)
            taken = subsetSumUtil(ind-1,target-arr[ind],arr,dp);

        return dp[ind][target]= notTaken||taken;
    }
    bool canPartition(vector<int> &nums)
    {
        int n = nums.size();
        int totSum=0;

        for(int i=0; i<n;i++){
            totSum+= nums[i];
        }

        if (totSum%2==1) return false;

        else
        {
            int k = totSum/2;
            vector<vector<int>> dp(n,vector<int>(k+1,-1));
            return subsetSumUtil(n-1,k,nums,dp);
        } 
    }
};
```


## Approach 2 [Dynamic Programming] :- 

```cpp
// Time Complexity - O(n*sum)
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
