31-12-2025  15:53

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Cheapest Flights Within K Stops

https://leetcode.com/problems/cheapest-flights-within-k-stops/

- Maintain a queue with stops, cost and node.
- Perform BFS, but only add the adjacent nodes if the current stop is <= k and the cost to reach there is < the stored one.

```cpp
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        queue<pair<int, pair<int, int>>> q;
        vector<vector<pair<int, int>>> adj(n);
        vector<int> costs(n, INT_MAX);
		
        for(auto it: flights) {
            adj[it[0]].push_back({it[1], it[2]});
        }
		
        costs[src] = 0;
        q.push({0, {0, src}});
		
        while(!q.empty()) {
            auto top = q.front();
            int stops = top.first;
            int cost = top.second.first;
            int node = top.second.second;
            q.pop();
			
            if(stops > k) {
                continue;
            }
			
            for(auto it: adj[node]) {
                int adjNode = it.first;
                int adjWeight = it.second;
				
                if(cost + adjWeight < costs[adjNode]) {
                    q.push({stops + 1, {cost + adjWeight, adjNode}});
                    costs[adjNode] = cost + adjWeight;
                }
            }
        }
		
        return costs[dst] == INT_MAX ? -1 : costs[dst];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(E)$        |     $O(2N + E)$      |





# References