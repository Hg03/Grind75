[Problem Statement](https://leetcode.com/problems/sort-colors/)

```cpp
// Time Complexity - O(n)               Space Complexity - O(1)
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n = 0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]==0){
                int temp = nums[i];
                nums[i] = nums[n];
                nums[n] = temp;
                n++;
            }
        }
        for(int i=0;i<nums.size();i++){
            if(nums[i]==1){
                int temp = nums[i];
                nums[i] = nums[n];
                nums[n] = temp;
                n++;
            }
        }
    }
};
```
