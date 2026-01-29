20-01-2026  15:59

Status: #Revision 

Tags: [[Tags/DSA]] [[Graphs]]

# Kosaraju's Algorithm

https://www.naukri.com/code360/problems/count-strongly-connected-components-kosaraju-s-algorithm_1171151

- We want to start from the 1st SCC so that we can differentiate between 2 SCC by visiting the first one first and stopping the traversal when 2nd SCC tries to go to 1st. 
- To find the first SCC perform DFS with a stack which pushes elements to the stack only when the entire subgraph is traversed.
- Then reverse all the edges of the graph. ( Reversing edges doesn't affect SCC but do affect the edge that connects them )
- Perform DFS again based on the ordering of the SCC and count connected components which will be the total SCC.

```cpp
#include <stack>

void findOrder(int node, int v, stack<int>& order, vector<int>& visited, vector<vector<int>>& adj) {
	visited[node] = 1;
	
	for(auto it: adj[node]) {
		if(!visited[it]) {
			findOrder(it, v, order, visited, adj);
		}
	}
	
	order.push(node);
}

void DFS(int node, int v, vector<int>& visited, vector<vector<int>>& adj) {
	visited[node] = 1;
	
	for(auto it: adj[node]) {
		if(!visited[it]) {
			DFS(it, v, visited, adj);
		}
	}
}

int stronglyConnectedComponents(int v, vector<vector<int>> &edges)
{
	vector<vector<int>>adj(v);
	vector<int>visited(v);
	stack<int> order;
	
	for(auto& it: edges) {
		adj[it[0]].push_back(it[1]);
	}
	
	for(int i = 0; i < v; i++) {
		if(!visited[i]) {
			findOrder(i, v, order, visited, adj);
		}
	}
	
	adj.clear();
	visited.clear();
	
	adj.resize(v);
	visited.resize(v);
	
	for(auto& it: edges) {
		adj[it[1]].push_back(it[0]);
	}
	
	int scc = 0;
	while(!order.empty()) {
		int node = order.top();
		order.pop();
		
		if(!visited[node]) {
			DFS(node, v, visited, adj);
			scc++;
		}
	}
	
	return scc;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(3 * (V + E))$   |   $O(2N + V + E)$    |





# References