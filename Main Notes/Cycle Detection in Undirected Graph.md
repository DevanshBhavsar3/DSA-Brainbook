25-11-2025  18:09

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Cycle Detection in Undirected Graph

https://www.naukri.com/code360/problems/cycle-detection-in-undirected-graph_1062670

### BFS

- For all the separated components in the graph run the bfs traversal.
- While traversing in the bfs, if some node is already visited and it is not the parent node of the current element, then there is a cycle.

> Because when there is a cycle, you will find pushing same node twice to the queue.

```cpp
#include <bits/stdc++.h>

bool traverse(int start, vector<vector<int>>& adj, queue<pair<int, int>>& q, vector<int>& visited) {
    q.push({start, -1});
    visited[start] = 1;
	
    while(!q.empty()) {
        pair<int, int> el = q.front();
        q.pop();
		
        for(auto it: adj[el.first]) {
            if(!visited[it]) {
                q.push({it, el.first});
                visited[it] = 1;
            } else if(it != el.second) {
                return true;
            }
        }
    }
	
    return false;
}

string cycleDetection (vector<vector<int>>& edges, int n, int m)
{
    vector<vector<int>> adj(n + 1);
    vector<int> visited(n + 1);
    queue<pair<int, int>> q;
	
    for(int i = 0; i < edges.size(); i++) {
        int u = edges[i][0];
        int v = edges[i][1];
		
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

	// O(N)
    for(int i = 1; i < visited.size(); i++) {
        if(!visited[i]) {
			// O(N + 2E)
            if(traverse(i, adj, q, visited)) {
                return "Yes";
            }
        }
    }
	
    return "No";
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(2N + 2E)$     |     $O(2N + 2E)$     |





# References