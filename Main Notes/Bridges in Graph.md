18-01-2026  15:43

Status: #Revision

Tags: [[Tags/DSA]] [[Graphs]]

# Bridges in Graph

https://leetcode.com/problems/critical-connections-in-a-network/

- Perform DFS while storing the current time and lowest time the node can visit.
- To calculate the lowest time go across all the adjacent node **except parent**, and calculate the minimum.
- If the lowest time an adjacent node can reach is > current node's time, that will be the critical edge, because that mean you have to pass through the current node to reach that node.

> This algorithms simply check if there exists a different path that leads to the time that is <= current node. If such path exists the current edge is not critical edge.

```cpp
class Solution {
public:
    void dfs(int node, int t, int parent, int n, vector<int>& time, vector<int>& low, vector<int>& visited, vector<vector<int>>& adj, vector<vector<int>>& critical) {
        visited[node] = 1;
        time[node] = low[node] = t;
		
        for(auto& it: adj[node]) {
            if(it == parent) {
                continue;
            }
			
            if(!visited[it]) {
                dfs(it, t + 1, node, n, time, low, visited, adj, critical);
            }
			
            low[node] = min(low[node], low[it]);
			
            if(low[it] > time[node]) {
                critical.push_back({it, node});
            }
        }
    }
	
    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& connections) {
        vector<vector<int>> critical, adj(n);
        vector<int> time(n), low(n), visited(n);
		
        for(auto& it: connections) {
            int u = it[0];
            int v = it[1];
			
            adj[u].push_back(v);
            adj[v].push_back(u);
        }
		
        dfs(0, 1, -1, n, time, low, visited, adj, critical);
		
        return critical;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(V + 2E)$     | $O(V + 2E) + O(3N)$  |





# References