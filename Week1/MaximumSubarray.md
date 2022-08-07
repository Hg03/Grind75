[Problem Statement](https://leetcode.com/problems/maximum-subarray/)

## Approach 1 :- Brute force approach - First we'll iterate the elements and its subarray with nested loops and another nested inside to calculate the sum of the subarrays and finds it maximum.

```cpp
//Time complexity - O(n^3)           Space Complexity - O(1)
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        int maximum = INT_MIN;
        for(int i=0;i<n;i++){
            for(int j=i;j<n;j++){
                int sum = 0;
                for(int k=i;k<=j;k++){
                    sum += nums[k];
                }
                if(sum > maximum) maximum = sum;
            }
        }
        return maximum;
    }
};
```

## Approach 2 :- Optimized 1st approach, we've reduced third loop to count sum individually.

```cpp
// Time Complexity - O(n^2)          Space Complexity - O(1)
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        int maxSum = 0;
        for(int i=0;i<n;i++)
        {
            int sum = 0;
            for(int j=i;j<n;j++)
            {
                sum+=nums[j];
                maxSum = max(maxSum,sum);
            }
        
        }
        return maxSum;
    }
};
```

## Approach 3 [Kadane's algorithm] :- In this approach, we'll traverse array once and keep track of max and sum using some conditions which are :
First assign first element to max and sum's value is 0 and then start traversing.
- Now check sum < 0, assign 0 to sum if not add the value at which pointer stay.
- Check maximum of sum in max variable.

```cpp
// Time complexity - O(n)      Space Complexity - O(1)
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        int sum = 0;
        int maxSum = INT_MIN;
        for(int i=0;i<n;i++)
        {
            sum+=nums[i];
            maxSum = max(maxSum,sum);
            if(sum < 0) sum = 0;
        }
        return maxSum;
    }
};
};
```
