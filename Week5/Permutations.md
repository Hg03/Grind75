[Problem Statement](https://leetcode.com/problems/permutations/)

[Refer this](https://youtu.be/pxA6l1X4iPU)

Intuition :- In this approach, we take one element at a time, and swap with itself then further next elements recursively and store its result in ans vector.

![alt text](https://github.com/Hg03/Grind75/blob/main/imgs/permutations.gif)

```cpp
class Solution {
public:
    void perm(vector<int>& nums,int i,vector<vector<int>>& ans)
    {
        if(i==nums.size())
        {
            ans.push_back(nums);
            return;
        }
        for(int j=i;j<nums.size();j++)
        {
            swap(nums[i],nums[j]);
            perm(nums,i+1,ans);
            swap(nums[i],nums[j]);
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ans;
        perm(nums,0,ans);
        return ans;
    }
};
```
