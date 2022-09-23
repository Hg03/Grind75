[Problem Statement](https://leetcode.com/problems/unique-paths/)

## Approach 1 [Recursive] :- In this, we'll traverse each possible path using recursion (incrementing i once then incrementing j once) by keeping in mind about border conditions.

```cpp
// Time Complexity - O(m x n)        Space Complexity - O(m x n)
class Solution {
public:
    int dfs(int i, int j, int m, int n, vector<vector<int>> &dp)
    {
        if(i==m||j==n){
            return 0;
        }
        if(i==m-1||j==n-1){
            return 1;
        }
        if(dp[i][j]!=-1){
            return dp[i][j];
        }
        return dp[i][j] = dfs(i+1,j,m,n,dp)+dfs(i,j+1,m,n,dp);
    }
    int uniquePaths(int m, int n)
    {
        vector<vector<int>> dp(m,vector<int>(n,-1));
        return dfs(0,0,m,n,dp);
    }
};
```

## Approach 2 [Optimized approach] :- In this, we use combinatorics approach. Watch [this](https://youtu.be/t_f0nwwdg5o) video for sure.

```cpp
// Time Complexity - O(m-1) or O(n-1)        Space Complexity - O(1)
class Solution {
public:
    int uniquePaths(int m, int n)
    {
        int N = n + m -2;
        int r = m - 1;
        double res = 1;
        for(int i=1;i<=r;i++)
        {
            res = res * (N - r + i)/i;
        }
        
        return (int)res;
    }
};
```
