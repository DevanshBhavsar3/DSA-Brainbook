07-01-2026  15:04

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Prim's Algorithm

https://www.naukri.com/code360/problems/minimum-spanning-tree_631769

- Keep a priority queue to process short weighted edges first.
- If the top node of the pq is not visited, mark it as visited and add the weight and edge if required.
- Add the adjacent edges of the node to the priority queue, if they are not visited. 

> Basically we are pushing all the edges to the priority queue.
> And the priority queue make sure that the edges with the least weight are processed first.

```cpp
#include <bits/stdc++.h>

int minimumSpanningTree(vector<vector<int>>& edges, int n)
{
	// O(E)
	priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
	vector<vector<pair<int, int>>> adj(n);
	vector<int> visited(n, 0);
	
	int mstSum = 0;
	
	for(auto& edge: edges) {
		int u = edge[0];
		int v = edge[1];
		int wt = edge[2];
		adj[u].push_back({v, wt});
		adj[v].push_back({u, wt});
	}
	
	pq.push({0, 0});

	// O(E)
	while(!pq.empty()) {
		// O(log E)
		auto top = pq.top();
		int wt = top.first;
		int node = top.second;
		pq.pop();
		
	    if(visited[node]) {
		    continue;
	    }
		
	    visited[node] = 1;
	    mstSum += wt;
	    // add edge to container if the question states

		// O(E)
	    for(pair<int, int>& it: adj[node]) {
		    if(!visited[it.first]) {
				// O(log E)
			    pq.push({it.second, it.first});
		    }
		}
	}
	  
	return mstSum;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(E \log E)$    |      $O(V + E)$      |
Excluding Adjacency List





# References