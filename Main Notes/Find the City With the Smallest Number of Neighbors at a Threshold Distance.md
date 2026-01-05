05-01-2026  15:35

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Find the City With the Smallest Number of Neighbors at a Threshold Distance

https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/

- Perform Dijkstra's algorithm considering every node as a source.
- Count the cities with distance <= distanceThreshold.
- Return the city with the smallest count.

```cpp
class Solution {
public:
    int dijkstra(int n, int src, vector<vector<pair<int, int>>>& adj, int distanceThreshold) {
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        vector<int> distance(n, INT_MAX);
		
        distance[src] = 0;
        pq.push({0, src});
		
        while(!pq.empty()) {
            auto [dist, node] = pq.top();
            pq.pop();
			
            for(auto& it: adj[node]) {
                int adjNode = it.first;
                int adjWeight = it.second;
                int newDist = dist + adjWeight;
				
                if(newDist < distance[adjNode] && newDist <= distanceThreshold) {
                    distance[adjNode] = newDist;
                    pq.push({distance[adjNode], adjNode});
                }
            }
        }
		
        int cnt = 0;
		
        for(auto& it: distance) {
            if(it != INT_MAX) {
                cnt++;
            }
        }
		
        return cnt;
    }
	
    int findTheCity(int n, vector<vector<int>>& edges, int distanceThreshold) {
        vector<vector<pair<int, int>>> adj(n);
		
        for(auto& edge: edges) {
            int u = edge[0];
            int v = edge[1];
            int wt = edge[2];
			
            adj[u].push_back({v, wt});
            adj[v].push_back({u, wt});
        }
		
        int city = -1;
        int cityCount = INT_MAX;
		
        for(int i = 0; i < n; i++) {
            int cnt = dijkstra(n, i, adj, distanceThreshold);
			
            if(cnt <= cityCount) {
                cityCount = cnt;
                city = i;
            }
        }
		
        return city;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(V * E \log V)$  |       $O(2V)$        |
Excluding Adjacency List


> Can be solved using Floyd Warshal Algorithm, but since the graph doesn't contain negative cycle, Dijkstra is better.





# References