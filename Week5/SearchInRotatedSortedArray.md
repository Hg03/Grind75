[Problem Statement](https://leetcode.com/problems/search-in-rotated-sorted-array)

## Approach 1 :- Here we can apply linear search which takes O(n) time, but thats not enough. 
## Approach 2 [Binary Search] :- Here we are applying binary search in unsorted array(kinda we can say) using following conditions.
1. First find mid as we do always in binary search algorithm
2. Now we find mid and check its leftmost element, and if it is smaller, array is sorted then check does element exist between that sorted part if yes shift your right pointer(mid-1) or else shift to left and do again this checking.

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int low = 0, high = nums.size()-1;
        while(low<=high)
        {
            int mid = low + (high-low)/2;
            if(nums[mid] == target) return mid;
            
            // check left side is sorted or not
            if(nums[low] <= nums[mid])
            {
                if(target >= nums[low] && target <= nums[mid])
                {
                    high = mid-1;
                }
                else
                    low = mid+1;
            }
            else
            {
                if(target >= nums[mid] && target <= nums[high])
                {
                    low = mid+1;
                }
                else
                    high = mid-1;
            }
        }
        return -1;
    }
};
```
