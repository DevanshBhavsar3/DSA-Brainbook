04-01-2026  13:56

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Floyd Warshal Algorithm

https://www.naukri.com/code360/problems/floyd-warshall_2041979

- Create a cost matrix, that will store the cost to go from u to v.
- For every pair of nodes, calculate the distance to the destination via every other node. 
- If the shortest path from the node to itself is < 0, then the graph contains negative cycles.

```cpp
int floydWarshall(int n, int m, int src, int dest, vector<vector<int>> &edges) {
    vector<vector<int>> cost(n + 1, vector<int>(n + 1, 1e9));
	
    for(int i = 1; i <= n; i++) {
        cost[i][i] = 0;
    }
	
    for(auto& it: edges) {
        int u = it[0];
        int v = it[1];
        int wt = it[2];
		
        cost[u][v] = wt;
    }
	
    for(int via = 1; via <= n; via++) {
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= n; j++) {
                if(cost[i][via] != 1e9 && cost[via][j] != 1e9) {
                    cost[i][j] = min(cost[i][j], cost[i][via] + cost[via][j]);
                }
            }
        }
    }
	
    return cost[src][dest];
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^3)$       |       $O(N^2)$       |





# References