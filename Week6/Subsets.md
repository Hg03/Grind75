[Problem Statement](https://leetcode.com/problems/subsets/)

Approach :- In this approach, we'll iterate through elements of array and take element or do not take element then eventually find its all subsets.

```cpp
// Time Complexity - O(2^N)         Space Complexity - O(2^N)
class Solution {
public:
    void help(int i,vector<int>& nums,vector<int>& temp,vector<vector<int>>& ans)
    {
        if(i==nums.size())
        {
            // When we reach to end, we'll push the result to ans array to return it.
            ans.push_back(temp);
        }
        else
        {
            // taken the element
            temp.push_back(nums[i]);
            help(i+1,nums,temp,ans);
            // Not taken the element
            temp.pop_back();
            help(i+1,nums,temp,ans);
        }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ans;
        vector<int> temp;
        help(0,nums,temp,ans);
        return ans;
    }
};
```
