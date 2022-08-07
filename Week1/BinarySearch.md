[Problem Statement](https://leetcode.com/problems/binary-search/)

## Iterative approach with O(logn) time complexity and O(1) space complexity

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int n = nums.size();
        int start = 0;
        int end = n-1;
        while(start<=end)
        {
            int mid = start + (end-start)/2;
            if(target == nums[mid]) return mid;
            else if(target < nums[mid]) end = mid-1;
            else start = mid+1;
        }
        return -1;
    }
};
```

## Recursive approach with also same as above complexities

```cpp
class Solution {
public:
    int searchRec(vector<int>& nums,int start,int end, int target) {
        while(start<=end)
        {
            int mid = start + (end-start)/2;
            if(target == nums[mid]) return mid;
            else if(target < nums[mid]) return searchRec(nums,start,mid-1,target);
            else return searchRec(nums,mid+1,end,target);
        }
        return -1;
    }
    int search(vector<int>& nums,int target)
    {
        return searchRec(nums,0,nums.size()-1,target);
    }
};
```
