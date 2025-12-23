23-12-2025  16:50

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Cycle Detection in Directed Graph (BFS)

https://www.naukri.com/code360/problems/detect-cycle-in-a-directed-graph_1062626

- Perform topo sort.
- If all the nodes are processed, then there is no cycles.

```cpp
#include <bits/stdc++.h>

int detectCycleInDirectedGraph(int n, vector < pair < int, int >> & edges) {
	vector<vector<int>> adj(n + 1);
	vector<int> indegree(n + 1);
	queue<int> q;
	int cnt = 0;
	
	for(int i = 0; i < edges.size(); i++) {
		int u = edges[i].first;
		int v = edges[i].second;
		
		adj[u].push_back(v);
		indegree[v]++;
	}
	
	for(int i = 1; i <= n; i++) {
		if(indegree[i] == 0) {
		    q.push(i);
		}
	}

	// O(N + E)
	while(!q.empty()) {
		int node = q.front();
		q.pop();
		
		cnt++;
		
		for(auto it: adj[node]) {
			indegree[it]--;
			
		    if(indegree[it] == 0) {
		        q.push(it);
			}
		}
	}
	
	return cnt != n;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(2N+E)$      |       $O(2N)$        |
Excluding Adjacency List





# References
[[Kahn's Algorithm]]