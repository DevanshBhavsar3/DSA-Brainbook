17-01-2026  10:17

Status: #Revision 

Tags: [[Tags/DSA]] [[Graphs]]

# Making A Large Island

https://leetcode.com/problems/making-a-large-island/

- First connect all the 1's in the disjoint set.
- While connecting keep track of largest component. (For handling case if the grid has only 1's).
- Then iterate over all the 0's and find the largest component size as if it was 1. 

```cpp
class DisjointSet {
public:
    vector<int> parent, size;
	
    DisjointSet(int n) {
        parent.reserve(n);
        size.resize(n, 1);
		
        for(int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
	
    int findParent(int node) {
        if(parent[node] == node) {
            return node;
        }
		
        return parent[node] = findParent(parent[node]);
    }
	
    void unionBySize(int u, int v) {
        int pU = findParent(u);
        int pV = findParent(v);
		
        if(pU == pV) {
            return;
        }
		
        if(size[pU] < size[pV]) {
            parent[pU] = pV;
            size[pV] += size[pU];
        } else {
            parent[pV] = pU;
            size[pU] += size[pV];
        }
    }
};


class Solution {
private:
    bool isValid(int nx, int ny, int n) {
        return nx >= 0 && nx < n && ny >= 0 && ny < n;
    }
public:
	
    int largestIsland(vector<vector<int>>& grid) {
        int n = grid.size();
		
        DisjointSet ds(n * n);
        int largest = 0;
		
        int dx[] = {-1, 0, 1, 0};
        int dy[] = {0, 1, 0, -1};
		
        // Connect all the components
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(grid[i][j] == 0) {
                    continue;
                }
				
                for(int k = 0; k < 4; k++) {
                    int nx = j + dx[k];
                    int ny = i + dy[k];
					
                    if(isValid(nx, ny, n) && grid[ny][nx]) {
                        int u = (i * n) + j;
                        int v = (ny * n) + nx;
						
                        ds.unionBySize(u, v);
                    }
                }
				
                int pU = ds.findParent((i * n) + j);
                largest = max(largest, ds.size[pU]);
            }
        }
		
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(grid[i][j]) {
                    continue;
                }
				
                map<int, int> mp;
                int size = 1;
				
                for(int k = 0; k < 4; k++) {
                    int nx = j + dx[k];
                    int ny = i + dy[k];
					
                    if(isValid(nx, ny, n) && grid[ny][nx]) {
                        int u = (ny * n) + nx;
                        int pU = ds.findParent(u);
						
                        if(mp.find(pU) == mp.end()) {
                            size += ds.size[pU];
                            mp[pU] = 1;
                        }
                    }
                }
				
                largest = max(largest, size);
            }
        }
		
        return largest;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(2*N^2*4)$     |     $O(2 * N^2)$     |





# References