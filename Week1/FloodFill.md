[Problem Statement](https://leetcode.com/problems/flood-fill)

## Approach :- In this approach, we'll perform dfs in image matrix where we color the box(means changing the previous value to newColor) and recursively iterate to up,down,right and left. For this, we have some base conditions which are -
- To stop recursion, when we reach top border.
- To stop recursion, when we reach down border.
- To stop recursion, when we reach left border.
- To stop recursion, when we reach right border.
- To stop recursion, when we reach different color(different from previous).
- To stop recursion, when we reach to a cell which is already colored.

```cpp
// Time Complexity - O(n)      Space Complexity - O(n)
class Solution {
public:
    void dfs(vector<vector<int>>& image, int r, int c, int color, int newColor)
    {
        if(image[r][c] == color)
        {
            image[r][c] = newColor;
            if(r >= 1) dfs(image,r-1,c,color,newColor);
            if(c >= 1) dfs(image,r,c-1,color,newColor);
            if(r+1 < image.size()) dfs(image,r+1,c,color,newColor);
            if(c+1 < image[0].size()) dfs(image,r,c+1,color,newColor);
        }
    }
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
       int color = image[sr][sc];
        if(color!= newColor) dfs(image,sr,sc,color,newColor);
        return image;
    }
};
```
