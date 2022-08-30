[Problem Statement](https://leetcode.com/problems/spiral-matrix)

## Approach - In this approach, we will create four pointer left, right, top and bottom. Then we start traversing left to right, when reaches to end, increment top, then traverse top to bottom, when reaches to end, decrement right, then traverse right to left, when reaches to end, decrement bottom and then traverse bottom to top, increment left.

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int left = 0;
        int top = 0;
        int right = matrix[0].size() - 1;
        int bottom = matrix.size() - 1;
        
        vector<int> result;
        
        while (top <= bottom && left <= right) {
            for (int j = left; j <= right; j++) {
                result.push_back(matrix[top][j]);
            }
            top++;
            
            for (int i = top; i <= bottom; i++) {
                result.push_back(matrix[i][right]);
            }
            right--;
            
            if (top <= bottom) {
                for (int j = right; j >= left; j--) {
                    result.push_back(matrix[bottom][j]);
                }
            }
            bottom--;
            
            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    result.push_back(matrix[i][left]);
                }
            }
            left++;
        }
        
        return result;
    }
};
```
