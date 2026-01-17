17-01-2026  11:30

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Swim in Rising Water

https://leetcode.com/problems/swim-in-rising-water/

## Dijkstra's Algorithm

- Perform Dijkstra's algorithm while maintaining the maximum cell value in the path.

```cpp
class Solution {
public:
    bool isValid(int nx, int ny, int n) {
        return nx >= 0 && nx < n && ny >= 0 && ny < n;
    }
	
    int swimInWater(vector<vector<int>>& grid) {
        int n = grid.size();
        priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, greater<pair<int, pair<int, int>>>> pq;
        vector<vector<int>> visited(n, vector<int>(n, 0));
		
        int dr[] = {-1, 1, 0, 0};
        int dc[] = {0, 0, -1, 1};
        
        pq.push({grid[0][0], {0, 0}});
        visited[0][0] = 1;
		
        while(!pq.empty()) {
            pair<int, pair<int, int>> top = pq.top();
            int wt = top.first;
            int row = top.second.first;
            int col = top.second.second;
            pq.pop();
			
            if(row == n - 1 && col == n - 1) {
                return wt;
            }
			
            for(int i = 0; i < 4; i++) {
                int nr = row + dr[i];
                int nc = col + dc[i];
				
                if(isValid(nr, nc, n) && !visited[nr][nc]) {
                    pq.push({max(wt, grid[nr][nc]), {nr, nc}});
                    visited[nr][nc] = 1;
                }
            }
        }
		
        return -1;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(N^2 \log N^2)$  |     $O(2 * N^2)$     |


## Kruskal's Algorithm

- Create edges from the grid.
- Find MST from source(0, 0) to destination(n, n) with Kruskal's Algorithms.
- While constructing the MST, if the ultimate parents of start and end becomes same, return the current weight.

```cpp
class DisjointSet {
private:
	vector<int> parent, size;
public:
	DisjointSet(int n) {
	    parent.resize(n);
	    size.resize(n, 1);
		
	    for (int i = 0; i < n; i++) {
		    parent[i] = i;
	    }
	}
	
	int findParent(int node) {
	    if (parent[node] == node) {
		    return node;
	    }
		
		parent[node] = findParent(parent[node]);
		
	    return parent[node];
	}
	
	void unionBySize(int u, int v) {
	    int pU = findParent(u);
	    int pV = findParent(v);
		
	    if (pU == pV) {
		    return;
	    }
		
	    if (size[pU] > size[pV]) {
			parent[pV] = pU;
			size[pU] += size[pV];
	    } else {
		    parent[pU] = pV;
		    size[pV] += size[pU];
	    }
	}
};

class Solution {
private:
    static bool comp(vector<int>& a, vector<int>& b) {
        return a[0] < b[0];
    }
public:
    int swimInWater(vector<vector<int>>& grid) {
        int n = grid.size();
		
        vector<vector<int>> edges;
        DisjointSet ds(n * n);
		
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(i > 0) {
                    int u = (i * n) + j;
                    int v = ((i - 1) * n) + j;
                    int wt = max(grid[i][j], grid[i - 1][j]);
					
                    edges.push_back({wt, u, v});
                }
				
                if(j > 0) {
                    int u = (i * n) + j;
                    int v = (i * n) + j - 1;
                    int wt = max(grid[i][j], grid[i][j - 1]);
					
                    edges.push_back({wt, u, v});
                }
            }
        }
		
        sort(edges.begin(), edges.end(), comp);
		
        for(auto it: edges) {
            int wt = it[0];
            int u = it[1];
            int v = it[2];
			
            ds.unionBySize(u, v);
			
            if(ds.findParent((n * n) - 1) == ds.findParent(0)) {
                return wt;
            }
        }
		
        return grid[0][0];
    }
};
```

|            **Time Complexity**             | **Space Complexity** |
| :----------------------------------------: | :------------------: |
| $O(N^2) + O(N^2 \log N^2) + O(N^2 \log N)$ |     $O(2 * N^2)$     |





# References