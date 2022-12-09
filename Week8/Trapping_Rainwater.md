[Problem Statement](https://leetcode.com/problems/trapping-rain-water/)

## Brute Force Approach :- In this approach, we'll find water content for each block or array index.
- First we'll find the left max and right max boundary for each element.
- Then we'll calculate minimum of both left max and right max.
- Then we'll subtract that element (height) from the minimum boundary calculated from 2nd step and update the answer.

```cpp
// Time Complexity - O(N^2)                Space Complexity - O(1)
class Solution {
public:
    int trap(vector<int>& height) {
        int ans = 0; // To store the answer
        for(int i = 0; i < height.size(); i++) 
        {
            int left_max = 0; // For calculation of max left boundary
            int right_max = 0; // For calculation of max right boundary
            
            // For left boundary
            for(int j = 0; j <= i; j++) 
            {
                if(height[j] > left_max) left_max = height[j]; 
            }
            
            // For right boundary
            for(int j = i; j < height.size(); j++)
            {    
                if(height[j] > right_max) right_max = height[j];
            }
            
            // Calculate the answer
            ans = ans + min(left_max, right_max) - height[i];
        }  
        return ans;
    }
};
```
## Better Approach - In this approach, we'll use two array which stores the left maximum for each element and right maximum for each element and then calculate the max water.

```cpp
// Time Complexity - O(N)              Space Complexity - O(N)
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size(), maxwater = 0;
        vector<int> prefmax(n),suffmax(n);
        prefmax[0] = height[0],suffmax[n-1] = height[n-1];
        
        for(int i = 1;i<n;i++) prefmax[i] = max(prefmax[i-1],height[i]); // Left max array
        for(int i = n-2;i>=0;i--) suffmax[i] = max(suffmax[i+1],height[i]); // Right max array
        
        // Calculation for max boundary
        for(int i = 0;i<n;i++)
        {
            maxwater += min(prefmax[i],suffmax[i]) - height[i];
        }
        return maxwater;
    }
};
```
## Optimized Approach - In this approach, we'll use two pointer approach and follow the below conditions :- 
- Initialize left(stand at beginning) and right(stand at end) pointers.
- Total water content is 0 initially.
- Initialize left max and right max also to be 0.
- If array[left] is less than or equal to array[right], then
1. If current element is greater than equal to leftmax, so update leftmax with current element.
2. Else 

```cpp
// Time Complexity - O(N)         Space Complexity - O(1)
class Solution {
public:
    int trap(vector<int>& height) {
        int l=0, r = height.size()-1, leftMax = INT_MIN, rightMax = INT_MIN, ans = 0;
        while(l<r) {
            if(height[l] <= height[r]) {
                if(height[l] > leftMax) {
                    leftMax = height[l];
                }
                else
                    ans += leftMax - height[l];
                l++;
            }
            else {
                if(height[r] > rightMax) {
                    rightMax = height[r];
                }
                else
                    ans += rightMax - height[r];
                r--;
            }
        }
        
        return ans;
    }
};
```
