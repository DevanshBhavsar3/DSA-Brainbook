03-01-2026  15:07

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Bellman Ford Algorithm

https://www.naukri.com/code360/problems/bellmon-ford_2041977

- Relax all the edges N - 1 times.
- Relaxation means updating the distance, if it is < than already present distance.

```cpp
vector<int> bellmonFord(int n, int m, int src, vector<vector<int>> &edges) {
    vector<int> distance(n + 1, 1e8);
        
    distance[src] = 0;
        
    for(int i = 0; i < n-1; i++) {
        for(auto edge: edges) {
            int u = edge[0];
            int v = edge[1];
            int wt = edge[2];
			
            if(distance[u] + wt < distance[v]) {
                distance[v] = distance[u] + wt;
            }
        }
    }
        
    return distance;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(V * E)$      |        $O(V)$        |


### Why N - 1 times?

![[Pasted image 20260103162203.png]]

In the worst case to update the last node you will have to iterate N - 1 times. Because there will be at max N - 1 edges from start to end. (It is impossible to create a graph that takes more than N - 1 edges to reach the end)


### How to check negative cycles?

After N - 1 iterations, if the distance array still updates, it means the graph have negative cycle.





# References