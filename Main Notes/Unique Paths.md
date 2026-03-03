14-02-2026  16:09

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Unique Paths

https://leetcode.com/problems/unique-paths/

## Memoization

- If you reach the last cell, return 1 (valid path).
- If any index is out of range return 0 (invalid path).
- Return the sum of the paths by going bottom and right.
- Memoize the path sum in a dp matrix.

```cpp
class Solution {
public:
    int find(int i, int j, int m, int n, vector<vector<int>>& dp) {
        if(i == m - 1 && j == n - 1) {
            return 1;
        } else if(i >= m || j >= n) {
            return 0;
        }
		
        if(dp[i][j] != -1) {
            return dp[i][j];
        }
		
        return dp[i][j] = find(i + 1, j, m, n, dp) + find(i, j + 1, m, n, dp);
    }
	
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, - 1));
		
        return find(0, 0, m, n, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(M*N)$       |   $O(M*N + (M+N))$   |


## Tabulation

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, 0));
		
        dp[0][0] = 1;
		
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(i == 0 && j == 0) {
                    continue;
                }
				
                dp[i][j] = ((i > 0) ? dp[i - 1][j] : 0) + ((j > 0) ? dp[i][j - 1] : 0);
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
    int uniquePaths(int m, int n) {
        vector<int> prev(n, 0);
		
        prev[0] = 1;
		
        for(int i = 0; i < m; i++) {
            vector<int> tmp(n, 0);
			
            for(int j = 0; j < n; j++) {
                tmp[j] = prev[j] + ((j > 0) ? tmp[j - 1]: 0);
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