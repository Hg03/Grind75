[Problem Statement](https://leetcode.com/problems/largest-rectangle-in-histogram/)

## Approach 1 :- In this approach, we'll simply use two for loops and traverse the whole array, then check for each block (element) and use another for loop to find minimum from left. Then eventually calculate the maximum rectangular area.

```cpp
// TLE code
class Solution {
public:
    int largestRectangleArea(vector <int> & heights) {
    int max_area = 0; // To calculate maximum rectangular area
    for (int i = 0; i < heights.size(); i++)
    {
        for (int j = i; j < heights.size(); j++)
        {
          int min_height = INT_MAX; // check for minimum height from starting uptil current element
          for (int k = i; k <= j; k++)
          {
              min_height = min(min_height, heights[k]);
          }
          max_area = max(max_area, min_height * (j - i + 1)); // Maximum area
        }
    }
    return max_area;
    }
};
```

## Approach 2 (using stack) :- In this, first we'll create two array ```left``` and ```right``` which stores left and right nearest smaller value for each element, then we'll calculate the maximum rectangular area.

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n = heights.size(); // size of array
        vector<int> x(n, n); // left
        vector<int> y(n, -1); // right
        stack<int> st;
        for (int i = 0; i < n; i++) {
            while (!st.empty() && heights[i] < heights[st.top()]) {
                x[st.top()] = i;
                st.pop();
            }
            st.push(i);
        }
        while (!st.empty())
            st.pop();
        for (int i = n-1; i >= 0; i--) {
            while (!st.empty() && heights[i] < heights[st.top()]) {
                y[st.top()] = i;
                st.pop();
            }
            st.push(i);
        }
        int ans = 0;
        for (int i = 0; i < n; i++) {
            ans = max(ans, (x[i] - y[i] - 1) * heights[i]);
        }
        return ans;
    }
};
```
