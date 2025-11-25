25-11-2025  17:07

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Flood Fill

https://leetcode.com/problems/flood-fill/

- Initially push the starting row and col to queue.
- Now push neighboring unvisited cells with same starting number to the queue, till it's not empty.
- Return the updated ans.

```cpp
class Solution {
public:
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        int m = image.size();
        int n = image[0].size();
		
        vector<vector<int>> ans;
        ans.insert(ans.begin(), image.begin(), image.end());
        queue<pair<int, int>> q;
		
        q.push({sr, sc});
        ans[sr][sc] = color;
		
        while(!q.empty()) {
            pair<int, int> el = q.front();
            q.pop();
			
            int dx[] = {-1, 1, 0, 0};
            int dy[] = {0, 0, -1, 1};
			
            for(int i = 0; i < 4; i++) {
                int ny = el.first + dy[i]; 
                int nx = el.second + dx[i];
				
                if(ny >= 0 && ny < m && nx >= 0 && nx < n && ans[ny][nx] != color && image[ny][nx] == image[sr][sc]) {
                    q.push({ny, nx});
                    ans[ny][nx] = color;
                }
            }
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $4*(M * N)$     |      $O(M * N)$      |





# References