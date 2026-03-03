16-02-2026  15:39

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Minimum Path Sum

https://leetcode.com/problems/minimum-path-sum/

## Memoization

- If you reach the last cell (0, 0), return its cost.
- If any index goes out of range return INT_MAX, so that it will never be considered as minimum path.
- Return the minimum sum of paths by going top and left.
- Memoize the minimum path sum in a dp matrix.

```cpp
class Solution {
public:
    int travel(int row, int col, vector<vector<int>>& grid, vector<vector<int>>& dp) {
        if(row == 0 && col == 0) {
            return grid[0][0];
        } else if(row < 0 || col < 0) {
            return INT_MAX;
        }
		
        if(dp[row][col] != -1) {
            return dp[row][col];
        }
		
        return dp[row][col] = min(
            travel(row - 1, col, grid, dp), 
            travel(row, col - 1, grid, dp)) + grid[row][col];
    }
	
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
		
        vector<vector<int>> dp(m, vector<int>(n, -1));
		
        return travel(m - 1, n - 1, grid, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(M*N)$       | $O(M*N) + O(M + N)$  |


## Tabulation

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
		
        vector<vector<int>> dp(m, vector<int>(n, -1));
		
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(i == 0 && j == 0) {
                    dp[i][j] = grid[0][0];
                    continue;
                }
				
                dp[i][j] = min(
                    ((i > 0) ? dp[i - 1][j] : INT_MAX), 
                    ((j > 0) ? dp[i][j - 1] : INT_MAX)) + grid[i][j];
            }
        }
		
        return dp[m - 1][n - 1];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(M*N)$       |       $O(M*N)$       |
### Space Optimization

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
		
        vector<int> prev(n, INT_MAX);
		
        for(int i = 0; i < m; i++) {
            vector<int> tmp(n);
			
            for(int j = 0; j < n; j++) {
                if(i == 0 && j == 0) {
                    tmp[j] = grid[i][j];
                    continue;
                }
				
                tmp[j] = min(
                    prev[j],
                    ((j > 0) ? tmp[j - 1] : INT_MAX)) + grid[i][j];
            }
			
            prev = tmp;
        }
		
        return prev[n - 1];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(M*N)$       |        $O(N)$        |





# References