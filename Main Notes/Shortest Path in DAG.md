26-12-2025  16:48

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Shortest Path in DAG

https://www.naukri.com/code360/problems/shortest-path-in-dag_8381897

- Perform topo sort and just store the elements in the stack.
- Find the minimum distance to all the adjacent nodes of top element of the stack until stack is empty.

> This algorithm first finds the linear order of the DAG, then update the distance sequentially starting from the first node in the order.

```cpp
void topoSort(int node, vector<int>& visited, vector<vector<pair<int, int>>>& adj, stack<int>& st) {
    visited[node] = 1;
	
    for(auto it: adj[node]) {
        if(!visited[it.first]) {
            topoSort(it.first, visited, adj, st);
        }
    }
	
    st.push(node);
}

vector<int> shortestPathInDAG(int n, int m, vector<vector<int>> &edges)
{
    vector<vector<pair<int, int>>> adj(n);
    stack<int> st;
    vector<int> visited(n);
    vector<int> distance(n, 1e9);
	
    for(int i = 0; i < edges.size(); i++) {
        adj[edges[i][0]].push_back({edges[i][1], edges[i][2]});
    }
	
	// O(N + M)
    for(int i = 0; i < n; i++) {
        if(!visited[i]) {
            topoSort(i, visited, adj, st);
        }
    }
	
    distance[0] = 0;
	
	// O(N + M)
    while(!st.empty()) {
        int node = st.top();
        st.pop();
		
        for(auto it: adj[node]) {
            if(distance[node] + it.second < distance[it.first]) {
                distance[it.first] = distance[node] + it.second;
            }
        }
    }
	
    for(int i = 0; i < n; i++) {
        if(distance[i] == 1e9) {
            distance[i] = -1;
        }
    }
	
    return distance;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O(2*(N + M))$    |     $O(5N + M)$      |


> Reason why simple BFS will not work:
> https://stackoverflow.com/a/74899496





# References