23-11-2025  18:24

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# BFS in Graph

https://www.naukri.com/code360/problems/bfs-in-graph_973002

- Create a queue and a visited arrays.
- Push the starting point in the queue and mark it as visited.
- Until queue is not empty get the front node and enqueue all the unvisited connected nodes.

```cpp
vector<int> bfsTraversal(int n, vector<vector<int>> &adj){
    vector<int> visited(n);
    vector<int> ans;
    queue<int> q;
	
    q.push(0);
    visited[0] = 1;
	
    while(!q.empty()) {
        int node = q.front();
        q.pop();
		
        ans.push_back(node);
		
		// O(2E) overall
        for(auto i: adj[node]) {
            if(!visited[i]) {
                visited[i] = 1;
                q.push(i);
            }
        }
    }
	
    return ans;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O(N) + O(2E)$    |       $O(3N)$        |





# References