30-12-2025  14:54

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Path with Minimum Effort

https://leetcode.com/problems/path-with-minimum-effort/

- Perform Dijkstra's algorithm, while storing the maximum effort taken in the path.
- Only visit the node if the effort to that node is minimum.
- If you reached the end node, return the effort.

```cpp
class Solution {
public:
    int minimumEffortPath(vector<vector<int>>& heights) {
        int n = heights.size();
        int m = heights[0].size();
		
        vector<vector<int>> effort(n, vector<int>(m, INT_MAX));
        priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, greater<pair<int, pair<int, int>>>> pq;
        
        int dy[] = {-1, 1, 0, 0};
        int dx[] = {0, 0, -1, 1};
		
        effort[0][0] = 0;
        pq.push({0, {0, 0}});
		
        while(!pq.empty()) {
            auto [eff, pos] = pq.top();
            int row = pos.first;
            int col = pos.second;
            pq.pop();
			
            if(row == n - 1 && col == m - 1) {
                return effort[n - 1][m - 1];
            }
			
            for(int i = 0; i < 4; i++) {
                int ny = row + dy[i];
                int nx = col + dx[i];
				
                if(ny >= 0 && ny < n && nx >= 0 && nx < m) {
                    int newEff = max(eff, abs(heights[row][col] - heights[ny][nx]));
					
                    if(newEff < effort[ny][nx]) {
                        pq.push({newEff, {ny, nx}});
                        effort[ny][nx] = newEff;
                    }
                }
            }
        }
		
        return effort[n - 1][m - 1];
    }
};
```

|             **Time Complexity**              | **Space Complexity** |
| :------------------------------------------: | :------------------: |
| $O(E \log V)$ or<br>$O(4 * N * M \log N* M)$ |      $O(N * M)$      |





# References
[[Dijkstra's Algorithm]]