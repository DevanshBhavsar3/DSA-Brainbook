27-11-2025  16:20

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Number of Enclaves

https://leetcode.com/problems/number-of-enclaves/

- For the 1's that does not end up at boundary, there shouldn't be a single 1 in the group, that is at the boundary.
- Traverse from all 1's that are at the boundary with DFS and mark them.
- All the other 1's will end up inside, so count them.

```cpp
class Solution {
public:
	// O(4 * M * N)
    void traverse(int i, int j, vector<vector<int>>& grid, vector<vector<int>>& visited) {
        int m = grid.size();
        int n = grid[0].size();
		
        visited[i][j] = 1;
		
        int dy[] = {-1, 1, 0, 0};
        int dx[] = {0, 0, -1, 1};
		
        for(int k = 0; k < 4; k++) {
            int nrow = i + dy[k];
            int ncol = j + dx[k];
			
            if(nrow >= 0 && nrow < m && ncol >= 0 && ncol < n && !visited[nrow][ncol] && grid[nrow][ncol] == 1) {
                traverse(nrow, ncol, grid, visited);
            }
        }
    }
	
    int numEnclaves(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
		
        vector<vector<int>> visited(m, vector<int>(n));
		
		// O(M)
        for(int i = 0; i < m; i++) {
            if(!visited[i][0] && grid[i][0] == 1) {
                traverse(i, 0, grid, visited);
            }
			
            if(!visited[i][n - 1] && grid[i][n - 1] == 1) {
                traverse(i, n - 1, grid, visited);
            }
        }
		
		// O(N)
        for(int i = 0; i < n; i++) {
            if(!visited[0][i] && grid[0][i] == 1) {
                traverse(0, i, grid, visited);
            }
			
            if(!visited[m - 1][i] && grid[m - 1][i] == 1) {
                traverse(m - 1, i, grid, visited);
            }
        }
		
        int total = 0;
		
		// O(M * N)
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(!visited[i][j] && grid[i][j]) {
                    total++;
                }
            }
        }
        
        return total;
    }
};
```

|        **Time Complexity**        | **Space Complexity** |
| :-------------------------------: | :------------------: |
| $O(M) + O(N) + O(M*N) + O(4*M*N)$ |     $O(2(M*N))$      |





# References