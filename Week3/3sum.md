[Problem Statement](https://leetcode.com/problems/3sum/)

## Approach 1 :- In this approach, we'll traverse the array using nested 3 for loop and check the sum i.e. 0. It takes lot of time taking O(n^3) time complexity.

## Approach 2 :- In this approach, we'll traverse the array to find first element and apply [two sum](https://github.com/Hg03/Grind75/blob/main/Week1/TwoSum.md) approach for remaining two elements.

```cpp
// Time Complexity - O(n^2)            Space Complexity - O(1)
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
      vector<vector<int>> output;
      sort(nums.begin(), nums.end());
      for(int i=0;i<nums.size();i++)
      {
          int a = nums[i];
          int other2 = -a;
          int s = i+1;
          int e = nums.size()-1;
          while(s<e)
          {
              if(nums[s] + nums[e] == other2)
              {
                  output.push_back({nums[i],nums[s],nums[e]});
                  while(s<e && nums[s] == nums[s+1]) s++;
                  while(s<e && nums[e] == nums[e-1]) e--;
                  s++;
                  e--;
              }
              else if(nums[s] + nums[e] < other2) s++;
              else e--;
          }
          while(i+1 < nums.size() && nums[i] == nums[i+1]) i++;
      }
      return output;
    }



};
```
