22-12-2025  17:14

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Kahn's Algorithm

https://www.naukri.com/code360/problems/topological-sort_982938

- Insert all the nodes with indegree of 0 to the queue.
- Push it to the ans and reduce adjacent node's indegree by 1.

> It is guaranteed that there will be minimum of 1 node with indegree of 0 at each iteration. 

> You are basically pushing elements to the ans before the element that have some indegrees.

```cpp
#include <bits/stdc++.h> 
vector<int> topologicalSort(vector<vector<int>> &edges, int v, int e)  {
    vector<int> ans;
    vector<int> indegree(v);
    vector<vector<int>> adj(v);
	
    for(int i = 0; i < edges.size(); i++) {
        int m = edges[i][0];
        int n = edges[i][1];
		
        adj[m].push_back(n);
        indegree[n]++;
    }
	
    queue<int> q;
	
    for(int i = 0; i < indegree.size(); i++) {
        if(indegree[i] == 0) {
            q.push(i);
        }
    }
		
	// O(N + E)
    while(!q.empty()) {
        int node = q.front();
        q.pop();
		
        ans.push_back(node);
		
        for(auto it: adj[node]) {
            indegree[it]--;
			
            if(indegree[it] == 0) {
                q.push(it);
            }
        }
    }
	
    return ans;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(2N + E)$     |       $O(3N)$        |
Excluding Adjacency List





# References