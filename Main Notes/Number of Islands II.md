13-01-2026  12:10

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Number of Islands II

https://www.naukri.com/code360/problems/number-of-islands-ii_1266048

- Consider every cell in the grid as a node of DSU.
- Loop through the queries and mark the cell as visited and increase the count for islands.
- If the cell has any neighboring cell which was visited, connect the current cell to that cell and decrease the island count.
- If both cells are already connected, don't decrease the island count.

```cpp
class DisjointSet {
public:
	vector<int> parent, size;
	
	DisjointSet(int n) {
		size.resize(n, 1);
		parent.reserve(n);
		
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

vector<int> numOfIslandsII(int n, int m, vector<vector<int>> &q){
	vector<vector<int>> visited(n, vector<int>(m, 0));
	DisjointSet ds(n * m);
	vector<int> islands;
	int cnt = 0;
	
	int dx[] = {-1, 1, 0, 0};
	int dy[] = {0, 0, -1, 1};
	
	for(auto& it: q) {
		int row = it[0];
		int col = it[1];
		
		if(visited[row][col]) {
			continue;
		}
		
		visited[row][col] = 1;
		cnt++;
		
		for(int i = 0; i < 4; i++) {
			int ny = row + dy[i];
			int nx = col + dx[i];
			
			if(ny >= 0 && ny < n && nx >= 0 && nx < m && visited[ny][nx]) {
				if(ds.findParent(row * m + col) != ds.findParent(ny * m + nx)) {
					ds.unionBySize(row * m + col, ny * m + nx);
					cnt--;
				}
			}
		}
		
		islands.push_back(cnt);
	}
	
	return islands;
}
```

|  **Time Complexity**  | **Space Complexity** |
| :-------------------: | :------------------: |
| $O(Q * 4 * 4 \alpha)$ |  $O(3 * N * M + Q)$  |





# References