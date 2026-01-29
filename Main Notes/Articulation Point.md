19-01-2026  14:50

Status: #Revision 

Tags: [[Tags/DSA]] [[Graphs]]

# Articulation Point

https://www.geeksforgeeks.org/problems/articulation-point-1/1

- Perform the same algorithm like [[Bridges in Graph]]. 
- Also, If the lowest time an adjacent node can reach is >= current node's time, and the current node is not the source, It is the articulation point.
- If the adjacent node is visited, meaning it is in the path, you will consider its insertion time not the lowest time to calculate the current nodes lowest time. Because what if that node is an articulation point, then you can't reach that node's lowest.
- If the source have multiple children, then the source is definitely the articulation point.
- Same node can be found as articulation point in multiple paths, so create an hash to store the points.

```cpp
class Solution {
  public:
    void DFS(int node, int t, int parent, int V, vector<int>& visited, vector<int>& time, vector<int>& low, vector<int> adj[], vector<int>& articulations) {
        visited[node] = 1;
        time[node] = low[node] = t;
        int child = 0;
        
        for(int& it: adj[node]) {
            if(it == parent) {
                continue;
            }
            
            if(!visited[it]) {
                DFS(it, t + 1, node, V, visited, time, low, adj, articulations);
                
                low[node] = min(low[node], low[it]);
				
				// Don't calculate for parent
                if(parent != -1 && low[it] >= time[node]) {
                    articulations[node] = 1;
                }
                
                child++;
            } else {
                low[node] = min(low[node], time[it]);
            }
            
        }
        
        if(parent == -1 && child > 1) {
            articulations[node] = 1;
        }
    }
	
    vector<int> articulationPoints(int V, vector<int> adj[]) {
        vector<int> time(V), low(V);
        vector<int> visited(V, 0);
        vector<int> articulations(V);
        
        for(int i = 0; i < V; i++) {
            if(!visited[i]) {
                DFS(0, 0, -1, V, visited, time, low, adj, articulations);
            }
        }
        
        vector<int> ans;
        
        for(int i = 0; i < V; i++) {
            if(articulations[i]) {
                ans.push_back(i);
            }
        }
        
        if(ans.size() == 0) {
            return {-1};
        }
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(2V + 2E)$     |       $O(4N)$        |





# References
[[Bridges in Graph]]