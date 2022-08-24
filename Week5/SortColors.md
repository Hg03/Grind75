[Problem Statement](https://leetcode.com/problems/sort-colors/)

## Approach 1 :- Using brute force, we can simply apply any sorting algorithm to sort the array. (Maybe merge, maybe counting etc..)

## Approach 2[Dutch National Flag] :- In this approach, we use 3 pointer i.e. low,mid and high. Low and mid on beginning and high on end of array. Move 3 pointer according to following conditions - 
**Iterate till mid <= hig**
- if mid's value == 2, then swap high's value with mid and decrement high.
- if mid's value == 0, then swap low's value with mid's value and increment low and mid = low+1.
- if mid's value == 1, then simply increment mid.

```cpp
// Time Complexity - O(n)               Space Complexity - O(1)
class Solution {

public:

    void sortColors(vector<int>& nums) {

        int low=0,high=nums.size()-1,mid=0;

        while(mid<=high)

        {

            if(nums[mid]==2)

            {

                swap(nums[high],nums[mid]);

                high--;

            }

            else if(nums[mid]==0)

            {

                swap(nums[mid],nums[low]);

                mid=low+1;

                low++;

            }

           else

               mid++;

        }

        

    }

};
```
