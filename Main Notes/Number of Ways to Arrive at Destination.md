01-01-2026  15:25

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Number of Ways to Arrive at Destination

https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/

- Perform Dijkstra's algorithm, but also store how many ways you can reach each node.
- If the distance to the nodes is the minimum, then the ways to reach that node will be the ways to reach the current node.
- But if the distance is equal, then you can increase the ways by the current node's way count.

```cpp
class Solution {
public:
    int countPaths(int n, vector<vector<int>>& roads) {
        priority_queue<pair<long, int>, vector<pair<long, int>>, greater<pair<long, int>>> pq;
        vector<vector<pair<int, int>>> adj(n);
        vector<long> distance(n, LONG_MAX);
        vector<int> ways(n, 0);
        int mod = (int) (1e9 + 7);
		
        for(auto& it: roads) {
            adj[it[0]].push_back({it[1], it[2]});
            adj[it[1]].push_back({it[0], it[2]});
        }
		
        distance[0] = 0;
        ways[0] = 1;
        pq.push({0, 0});
		
        while(!pq.empty()) {
            auto [dist, node] = pq.top();
            pq.pop();
			
            for(auto& it: adj[node]) {
                int adjNode = it.first;
                int adjWeight = it.second;
                long newDist = dist + adjWeight;
				
                if(newDist < distance[adjNode]) {
                    ways[adjNode] = ways[node];
                    distance[adjNode] = newDist;
                    pq.push({newDist, adjNode});
                } else if(newDist == distance[adjNode]) {
                    ways[adjNode] = (ways[adjNode] + ways[node]) % mod;
                }
            }
        }
		
        return ways[n - 1] % mod;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(E \log V)$    |      $O(V + E)$      |





# References