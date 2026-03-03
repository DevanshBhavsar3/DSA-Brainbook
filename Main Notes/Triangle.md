16-02-2026  16:23

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Triangle

https://leetcode.com/problems/triangle/

## Memoization

- If you reach the last row, return the value.
- Return the minimum sum of paths by going bottom and bottom right.
- Memoize the minimum path sum in a dp matrix.

```cpp
class Solution {
public:
    int find(int row, int col, vector<vector<int>>& triangle, vector<vector<int>>& dp) {
        if(row == triangle.size() - 1) {
            return triangle[row][col];
        }
		
        if(dp[row][col] != -1) {
            return dp[row][col];
        }
		
        return dp[row][col] = min(find(row + 1, col, triangle, dp), find(row + 1, col + 1, triangle, dp)) + triangle[row][col];
    }
	
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
		
        vector<vector<int>> dp(n, vector<int>(n, -1));
		
        return find(0, 0, triangle, dp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*N)$       |     $O(N*N + N)$     |


## Tabulation

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
		
        vector<vector<int>> dp(n, vector<int>(n, -1));
		
        for(int i = 0; i < n; i++) {
            dp[n - 1][i] = triangle[n - 1][i];
        }
		
        for(int i = n - 2; i >= 0; i--) {
            for(int j = 0; j < triangle[i].size(); j++) {
                dp[i][j] = min(dp[i + 1][j], dp[i + 1][j + 1]) + triangle[i][j];
            }
        }
		
        return dp[0][0];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*N)$       |       $O(N*N)$       |
### Space Optimization

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
		
        vector<int> prev(n + 1, 0);
		
        for(int i = n - 1; i >= 0; i--) {
            vector<int> tmp(n);
			
            for(int j = 0; j < triangle[i].size(); j++) {
                tmp[j] = min(prev[j], prev[j + 1]) + triangle[i][j];
            }
			
            prev = tmp;
        }
		
        return prev[0];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N*N)$       |        $O(N)$        |





# References