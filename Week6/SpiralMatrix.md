[Problem Statement](https://leetcode.com/problems/spiral-matrix)

## Approach - In this approach, we will create four pointer left, right, top and bottom. Then we start traversing left to right, when reaches to end, increment top, then traverse top to bottom, when reaches to end, decrement right, then traverse right to left, when reaches to end, decrement bottom and then traverse bottom to top, increment left.

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        // Maintain these 4 pointers
        int left = 0;
        int top = 0;
        int right = matrix[0].size() - 1;
        int bottom = matrix.size() - 1;
        
        vector<int> result;
        
        while (top <= bottom && left <= right)
        {
            // Here, we'll move onto row from left to right
            for (int j = left; j <= right; j++)
            {
                result.push_back(matrix[top][j]);
            }
            top++; // After the row ends, go down by increment top pointer
            
            // Now we'll go to last column of each spiral, therefore increment the row by row and store the last column element.
            for (int i = top; i <= bottom; i++)
            {
                result.push_back(matrix[i][right]); // Column is fixed, as it is always last
            }
            right--; // After the column end, we'll traverse the last row of spiral from right to left, as last element of last row is stored as last column's element
            
            // If we have big matrix (greater than 1 x 1)
            if (top <= bottom)
            {
                // Go traverse from right to left
                for (int j = right; j >= left; j--)
                {
                    result.push_back(matrix[bottom][j]); // Here, row is fixed.
                }
            }
            bottom--; // Now , we've to print first column from down to top, therefore decrement bottom
            
          
            if (left <= right)
            {
                // Now traverse the first column of spiral, from down to top
                for (int i = bottom; i >= top; i--)
                {
                    result.push_back(matrix[i][left]);
                }
            }
            
            left++; // Start traversing again from next spiral, matrix reduces to small size.
        }
        
        return result;
    }
};
```
