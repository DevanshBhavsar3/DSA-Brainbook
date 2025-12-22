20-12-2025  19:40

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Cycle Detection in Directed Graph

https://www.naukri.com/code360/problems/detect-cycle-in-a-directed-graph_1062626

- Perform DFS and store the visited and path visited array.
- If the node is visited and it is in the path return true.
- Remove the node from the path after the traversal.

```cpp
bool traverse(int node, vector<vector<int>>& adj, vector<int>& visited, vector<int>& path) {
	visited[node] = 1;
	path[node] = 1;
	
	for(auto it: adj[node]) {
		if(!visited[it]) {
			if(traverse(it, adj, visited, path)) {
				return true;
			}
		} else if(path[it]) {
			return true;
		}
	}
		
	path[node] = 0;
	return false;
}

int detectCycleInDirectedGraph(int n, vector < pair < int, int >> & edges) {
	vector<vector<int>> adj(n + 1, vector<int>());
	
	for(int i = 0; i < edges.size(); i++) {
		int u = edges[i].first;
		int v = edges[i].second;
		
		adj[u].push_back(v);
	}
	
	vector<int> visited(n + 1);
	vector<int> path(n + 1);
	
	for(int i = 1; i < n; i++) {
		if(!visited[i]) {
			// Overall O(N + E)
		    if(traverse(i, adj, visited, path)) {
		        return 1;
		    }
	    }
	}
	
	return 0;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(2N + E)$     |     $O(3N + E)$      |





# References