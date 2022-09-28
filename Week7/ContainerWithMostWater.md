[Problem Statement](https://leetcode.com/problems/container-with-most-water/)

## Approach 1 :- In this, we'll explore all pairs and finds maximum area from each two heights.

```cpp
// Time Complexity - O(n^2)            Space Complexity - O(1)
class Solution {
public:
    int maxArea(vector<int>& height) {
        int maxArea = INT_MIN;
        for(int i=0;i<height.size();i++)
        {
            for(int j=i+1;j<height.size();j++)
            {
                maxArea = max(maxArea, min(height[i],height[j])*(j-i));
            }
        }
        return maxArea;
    }
};
```

## Approach 2 :- In this, we'll use two variable i and j, starts from beginning and end respectively. Check the maxArea until i < j.

```cpp
// Time Complexity - O(logn)            Space Complexity - O(1)
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0;
        int right = height.size()-1;
        int area;
        int maxArea = INT_MIN;
        while(left < right)
        {
            area = min(height[left],height[right]) * (right-left);
            maxArea = max(maxArea,area);
            if(height[left] < height[right]) left++;
            else right--;
        }
        return maxArea;
    }
};
```
