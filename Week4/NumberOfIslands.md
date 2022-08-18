[Problem Statement](https://leetcode.com/problems/number-of-islands)

## Approach :- In this approach, we'll iterate through each cell if it's value is '1', then apply BFS means move four direction to 1 and check if there is also ,recursively iterate and make all the '1' set to '2' which indicates island is visited. Keep count of number of island parallely.

```cpp
// Time Complexity - O(m*n)           Space Complexity - O(m*n)
class Solution {
private:
    void mark_current_island(vector<vector<char>> &matrix, int x,int y,int r,int c)
    {
        if(x<0 || x>=r || y<0 || y>=c || matrix[x][y]!='1')
            return;
        
        matrix[x][y] = '2';
        mark_current_island(matrix,x+1,y,r,c);
        mark_current_island(matrix,x,y+1,r,c);
        mark_current_island(matrix,x-1,y,r,c);
        mark_current_island(matrix,x,y-1,r,c);
    }
public:
    int numIslands(vector<vector<char>>& grid) {
       int rows = grid.size();
        if(rows==0)
            return 0;
        int cols = grid[0].size();
        
        int no_of_islands = 0;
        for(int i=0;i<rows;i++)
        {
            for(int j=0;j<cols;j++)
            {
                if(grid[i][j] == '1')
                {
                    mark_current_island(grid,i,j,rows,cols);
                    no_of_islands++;
                }
            }
        }
        return no_of_islands;
    }
};
```
