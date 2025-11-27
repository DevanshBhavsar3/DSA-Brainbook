26-11-2025  15:52

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# 01 Matrix

https://leetcode.com/problems/01-matrix/

- Push all the 0's to the queue and perform bfs.
- Store the dist for each level and assign that to the ans.

```cpp
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int m = mat.size();
        int n = mat[0].size();
		
        vector<vector<int>> ans(m, vector<int>(n));
        vector<vector<int>> visited(m, vector<int>(n));
        queue<pair<pair<int, int>, int>> q;

		// O(M*N)
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(mat[i][j] == 0) {
                    q.push({{i, j}, 0});
                    visited[i][j] = 1;
                }
            }
        }
		
		// O(4*M*N)
        while(!q.empty()) {
            pair<pair<int, int>, int> node = q.front();
            q.pop();
            
            int i = node.first.first;
            int j = node.first.second;
            int d = node.second;
			
            ans[i][j] = d;
			
            int dy[] = {1, -1, 0, 0};
            int dx[] = {0, 0, 1, -1};
			
            for(int k = 0; k < 4; k++) {
                int ny = i + dy[k];
                int nx = j + dx[k];
				
                if(ny >= 0 && ny < m && nx >= 0 && nx < n && !visited[ny][nx]) {
                    q.push({{ny, nx}, d + 1});
                    visited[ny][nx] = 1;
                }
            }
        }
		
        return ans;   
    }
};
```

| **Time Complexity**  | **Space Complexity** |
| :------------------: | :------------------: |
| $O((M*N) + 4*(M*N))$ |     $O(3*(M*N)$      |





# References