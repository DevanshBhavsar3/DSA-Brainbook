14-02-2026  17:22

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Dynamic Programming]]

# Unique Paths II

https://leetcode.com/problems/unique-paths-ii/

- Same as the unique paths problems, but don't calculate the sum of path for the obstacle cell.
- So any other cell which tries to go through obstacle will get the sum of 0.

```cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
		
        vector<int> prev(n, 0);
        prev[0] = 1;
		
        for(int i = 0; i < m; i++) {
            vector<int> tmp(n);
			
            for(int j = 0; j < n; j++) {
                if(obstacleGrid[i][j]) {
                    continue;
                }
                
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
[[Unique Paths]]