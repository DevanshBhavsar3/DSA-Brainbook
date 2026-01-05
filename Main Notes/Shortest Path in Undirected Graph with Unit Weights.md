25-12-2025  16:29

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Shortest Path in Undirected Graph with Unit Weights

https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph-having-unit-distance/1

- Perform BFS from the source, while storing the distance with each node.
- If the distance is already calculated, then don't update it.

```cpp
class Solution {
  public:
    vector<int> shortestPath(int V, vector<vector<int>> &edges, int src) {
        vector<vector<int>> adj(V);
        vector<int> pathDistance(V, -1);
        queue<pair<int, int>> q;
        
        for(int i = 0; i < edges.size(); i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            
            adj[u].push_back(v);
            adj[v].push_back(u);
        }
        
        q.push({src, 0});
        pathDistance[src] = 0;
        
        while(!q.empty()) {
            pair<int, int> top = q.front();
            q.pop();
            
            int node = top.first;
            int distance = top.second;
            
            for(auto it: adj[node]) {
                if(pathDistance[it] == -1) {
                    q.push({it, distance + 1});
                    pathDistance[it] = distance + 1;
                }
            }
        }
        
        return pathDistance;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O(E + V + 2E)$   |     $O(3V + 2E)$     |





# References