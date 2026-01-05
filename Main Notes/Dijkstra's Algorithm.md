27-12-2025  17:32

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Dijkstra's Algorithm

>NOTE:
>Can't be used with negatively weighted graph.

https://www.naukri.com/code360/problems/dijkstra-s-shortest-path_920469

### Implementation using Priority Queue

- Store distance and node in priority queue (min heap).
- For every adjacent nodes, if the distance to that node is smaller, store it and add it to the priority queue.
- Min heap will greedily consider shorter paths first.

```cpp
#include <bits/stdc++.h> 
vector<int> dijkstra(vector<vector<int>> &vec, int vertices, int edges, int source) {
    vector<vector<pair<int, int>>> adj(vertices);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    vector<int> distance(vertices, INT_MAX);
	
    for(int i = 0; i < edges; i++) {
        int u = vec[i][0];
        int v = vec[i][1];
        int weight = vec[i][2];
		
        adj[u].push_back({v, weight});
        adj[v].push_back({u, weight});
    }
	
    distance[0] = 0;
    pq.push({0, 0});
	
    while(!pq.empty()) {
        pair<int, int> top = pq.top();
        pq.pop();
		
        int dist = top.first;
        int node = top.second;
		
        for(auto it: adj[node]) {
            int adjNode = it.first;
            int adjWeight = it.second;
			
            if(dist + adjWeight < distance[adjNode]) {
                pq.push({dist + adjWeight, adjNode});
                distance[adjNode] = dist + adjWeight;
            }
        }
    }
	
    return distance;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(E \log V)$    |       $O(2V)$        |
Excluding Adjacency List


### Implementation using Set

- Store distance and node in set.
- For every adjacent nodes, if the distance to that node is smaller, store it and add it to the set.
- With the set you can also remove longer path from the set.
- Set will store the shorter paths on the top automatically.

```cpp
#include <bits/stdc++.h> 
vector<int> dijkstra(vector<vector<int>> &vec, int vertices, int edges, int source) {
    vector<vector<pair<int, int>>> adj(vertices);
    set<pair<int, int>> st;
    vector<int> distance(vertices, INT_MAX);
	
    for(int i = 0; i < edges; i++) {
        int u = vec[i][0];
        int v = vec[i][1];
        int weight = vec[i][2];
		
        adj[u].push_back({v, weight});
        adj[v].push_back({u, weight});
    }
	
    st.insert({0, source});
    distance[source] = 0;
	
    while(!st.empty()) {
        pair<int, int> top = *st.begin();
        int dist = top.first;
        int node = top.second;
        st.erase(top);
		
        for(auto it: adj[node]) {
            int adjNode = it.first;
            int adjWeight = it.second;
			
            if(dist + adjWeight < distance[adjNode]) {
                // erase longer paths from the set
                if(distance[adjNode] != INT_MAX) {
                    st.erase({distance[adjNode], adjNode});
                }
                
                distance[adjNode] = dist + adjWeight;
                st.insert({dist + adjWeight, adjNode});
            }
        }
    }
	
    return distance;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(E \log V)$    |       $O(2V)$        |
Excluding Adjacency List


### Why Priority Queue and not Queue?

![[Screenshot From 2025-12-27 19-11-03.png]]

As shown in the diagram the priority queue will first consider shorter distance paths, resulting in less redundant traversal.

The queue will travel the same node twice unnecessary in case of 2 paths, resulting in greater time complexity.


### Time Complexity Analysis

```cpp
// O(V)
while(!pq.empty()) {
    pair<int, int> top = pq.top();
	// O(log HeapSize)
    pq.pop();
		
    int dist = top.first;
    int node = top.second;
	
	// O(V - 1) : If all nodes are connected to every other node
    for(auto it: adj[node]) {
        int adjNode = it.first;
        int adjWeight = it.second;
		
        if(dist + adjWeight < distance[adjNode]) {
			// O(log HeapSize)
            pq.push({dist + adjWeight, adjNode});
            distance[adjNode] = dist + adjWeight;
        }
    }
}
```

$O(V * (\log \text{Heap Size} + V -1 * \log \text{Heap Size}))$
$O(V * (\log \text{Heap Size} * (1 + V -1))$
$O(V * (\log \text{Heap Size} * (V))$
$O(V^2 * \log \text{Heap Size})$

If every node is connected with every other node, the maximum heap size could be $\approx O(V^2)$.

$O(V^2 * \log V^2)$
$O(V^2 * 2 \log V)$

If each node have $V - 1$ edges, then $V * (V - 1) = E$

$O(E * 2 \log V)$
$\approx O(E * \log V)$





# References