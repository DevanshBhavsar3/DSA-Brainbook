01-01-2026  15:03

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Network Delay Time

https://leetcode.com/problems/network-delay-time/

- Perform Dijkstra's algorithms.
- Return the maximum distance across all the node, if it is INT_MAX return -1.

```cpp
class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        vector<vector<pair<int, int>>> adj(n + 1);
        vector<int> distance(n + 1, INT_MAX);
		
        for(int i = 0; i < times.size(); i++) {
            adj[times[i][0]].push_back({times[i][1], times[i][2]});
        }
		
        distance[k] = 0;
        pq.push({0, k});
		
        while(!pq.empty()) {
            auto [dist, node] = pq.top();
            pq.pop();
			
            for(auto it: adj[node]) {
                int adjNode = it.first;
                int adjWeight = it.second;
				
                if(dist + adjWeight < distance[adjNode]) {
                    pq.push({dist + adjWeight, adjNode});
                    distance[adjNode] = dist + adjWeight;
                }
            }
        }
		
        int minimumTime = -1;
		
        for(int i = 1; i < distance.size(); i++) {
            minimumTime = max(minimumTime, distance[i]);
        }
		
        return minimumTime == INT_MAX ? -1: minimumTime;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(E \log V)$    |     $O(3V + E)$      |





# References