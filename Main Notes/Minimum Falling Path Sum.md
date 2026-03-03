03-03-2026  16:09

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Minimum Falling Path Sum

https://leetcode.com/problems/minimum-falling-path-sum/

## Memoization

- If you reach the last row, return the value.
- Return INT_MAX for invalid indexes.
- For all the paths starting from each element of the first row, return the minimum sum of path by going bottom and diagonally left/right.
- Memoize the minimum path sum in a dp matrix.

```cpp
class Solution {
public:
    int fall(int row, int col, vector<vector<int>>& matrix, vector<vector<int>>& dp) {
        if(col < 0 || col >= matrix.size()) {
            return INT_MAX;
        } else if(row == matrix.size() - 1) {
            return matrix[row][col];
        }
		
        if(dp[row][col] != -1) {
            return dp[row][col];
        }
		
        int mini = INT_MAX;
		
        mini = min(mini, fall(row + 1, col, matrix, dp));
        mini = min(mini, fall(row + 1, col - 1, matrix, dp));
        mini = min(mini, fall(row + 1, col + 1, matrix, dp));
		
        return dp[row][col] = mini + matrix[row][col];
    }
	
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
		
        vector<vector<int>> dp(n, vector<int>(n, -1));
        int mini = INT_MAX;
		
        for(int i = 0; i < n; i++) {
            mini = min(mini, fall(0, i, matrix, dp));
        }
		
        return mini;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |     $O(N^2 + N)$     |


## Tabulation

```cpp
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
		
        vector<vector<int>> dp(n, vector<int>(n, INT_MAX));
		
        for(int i = 0; i < n; i++) {
            dp[n - 1][i] = matrix[n - 1][i];
        }
        
        for(int i = n - 2; i >= 0; i--) {
            for(int j = 0; j < n; j++) {
                int mini = INT_MAX;
				
                mini = min(mini, dp[i + 1][j]);
				
                if(j > 0) {
                    mini = min(mini, dp[i + 1][j - 1]);
                }
				
                if(j < n - 1) {
                    mini = min(mini, dp[i + 1][j + 1]);
                }
				
                dp[i][j] = mini + matrix[i][j];
            }
        }
		
        int mini = INT_MAX;
        for(int i = 0; i < n; i++) {
            mini = min(mini, dp[0][i]);
        }
		
        return mini;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |       $O(N^2)$       |
### Space Optimization

```cpp
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
		
        vector<int> prev(n);
		
        for(int i = 0; i < n; i++) {
            prev[i] = matrix[n - 1][i];
        }
        
        for(int i = n - 2; i >= 0; i--) {
            vector<int> tmp(n);
			
            for(int j = 0; j < n; j++) {
                int mini = INT_MAX;
				
                mini = min(mini, prev[j]);
				
                if(j > 0) {
                    mini = min(mini, prev[j - 1]);
                }
				
                if(j < n - 1) {
                    mini = min(mini, prev[j + 1]);
                }
				
                tmp[j] = mini + matrix[i][j];
            }
            
            prev = tmp;
        }
		
        int mini = INT_MAX;
        for(int i = 0; i < n; i++) {
            mini = min(mini, prev[i]);
        }
		
        return mini;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(N)$        |





# References