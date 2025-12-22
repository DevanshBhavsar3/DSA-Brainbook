22-12-2025  16:42

Status: #Revision 

Tags: [[Index/DSA|DSA]] [[Graphs]]

# Topo Sort

https://www.naukri.com/code360/problems/topological-sort_982938

- Perform DFS and push elements to the stack after traversing all its adjacent nodes.
- Because you are pushing elements to the stack after traversing its adjacent nodes, it will come before all of its adjacent node in the ans.

```cpp
#include <bits/stdc++.h>

void traverse(int node, stack<int>& st, vector<int>& visited, vector<vector<int>>& adj) {
    visited[node] = 1;
	
    for(auto it: adj[node]) {
        if(!visited[it]) {
            traverse(it, st, visited, adj);
        }
    }
	
    st.push(node);
}

vector<int> topologicalSort(vector<vector<int>> &edges, int v, int e)  {
    vector<vector<int>> adj(v, vector<int>());
	
    for(int i = 0; i < edges.size(); i++) {
        int u = edges[i][0];
        int v = edges[i][1];
		
        adj[u].push_back(v);
    }
	
    stack<int> st;
    vector<int> visited(v);
	
    for(int i = 0; i < v; i++) {
        if(!visited[i]) {
			// Overall O(N + E)
            traverse(i, st, visited, adj);
        }
    }
	
    vector<int> ans;
	
    while(!st.empty()) {
        ans.push_back(st.top());
        st.pop();
    }
	
    return ans;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(3N + E)$     |       $O(4N)$        |
Excluding Adjacency List





# References