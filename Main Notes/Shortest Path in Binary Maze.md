29-12-2025  15:32

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Shortest Path in Binary Maze

https://leetcode.com/problems/shortest-path-in-binary-matrix/

- Perform normal BFS while storing the distance to every visited node.
- Only visit the cell with value 0 and distance that is less than the stored one. 
- If you reached the destination return the distance, else -1.

> We don't need priority queue here because the edge weight is constant 1, resulting in same behavior as queue.

```cpp
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        int n = grid.size();
		
        vector<vector<int>> distance(n, vector<int>(n, INT_MAX));
        queue<pair<int, pair<int, int>>> q;
		
        int dy[] = {0, 0, -1, 1, -1, -1, 1, 1};
        int dx[] = {-1, 1, 0, 0, -1, 1, -1, 1};
		
        if(grid[0][0] == 0) {
            q.push({1, {0, 0}});
            distance[0][0] = 1;
        }
		
        while(!q.empty()) {
            pair<int, pair<int, int>> top = q.front();
            q.pop();
			
            int dist = top.first;
            int row = top.second.first;
            int col = top.second.second;
			
            if(row == n - 1 && col == n - 1) {
                return dist;
            }
			
            for(int i = 0; i < 8; i++) {
                int ny = row + dy[i];
                int nx = col + dx[i];
				
                if(nx >= 0 && nx < n && ny >= 0 && ny < n && grid[ny][nx] == 0 && dist + 1 < distance[ny][nx]) {
                    q.push({dist + 1, {ny, nx}});
                    distance[ny][nx] = dist + 1;
                }
            }
        }
        
        return -1;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(8 * N^2)$     |      $O(2N^2)$       |





# References