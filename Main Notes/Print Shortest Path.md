28-12-2025  15:34

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Print Shortest Path

https://www.geeksforgeeks.org/problems/shortest-path-in-weighted-undirected-graph/1

- Store the minimum distance parent of every node.
- Perform Dijkstra's algorithms while storing the parent node every time the distance is updated.
- Construct shortest path by backtracking from last node.

```cpp
class Solution {
  public:
    vector<int> shortestPath(int n, int m, vector<vector<int>>& edges) {
        vector<vector<pair<int, int>>> adj(n + 1);
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        vector<int> parent(n + 1, -1);
        vector<int> distance(n + 1, INT_MAX);
        
        for(int i = 0; i < m; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            int weight = edges[i][2];
            
            adj[u].push_back({v, weight});
            adj[v].push_back({u, weight});
        }
        
        distance[1] = 0;
        pq.push({0, 1});
        
        while(!pq.empty()) {
            pair<int, int> top = pq.top();
            pq.pop();
            
            int dist = top.first;
            int node = top.second;
            
            for(auto it: adj[node]) {
                int adjNode = it.first;
                int adjWeight = it.second;
                
                if(dist + adjWeight < distance[adjNode]) {
                    parent[adjNode] = node;
                    distance[adjNode] = dist + adjWeight;
                    pq.push({dist + adjWeight, adjNode});
                }
            }
        }
        
        if(distance[n] == INT_MAX) {
            return {-1};
        }
        
        vector<int> path;
        int curr = n;
        
        while(curr != -1) {
            path.push_back(curr);
            curr = parent[curr];
        }
        
        path.push_back(distance[n]);
        
        reverse(path.begin(), path.end());
        
        return path;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(V + E \log V)$  |       $O(3V)$        |
Excluding Adjacency List





# References
[[Dijkstra's Algorithm]]