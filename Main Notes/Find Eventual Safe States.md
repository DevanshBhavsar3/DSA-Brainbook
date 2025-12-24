24-12-2025  16:24

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Find Eventual Safe States

https://leetcode.com/problems/find-eventual-safe-states/

- Reverse the edges of the graph.
- Terminal nodes don't have outdegree, so by reversing the edges of the graph, it won't have indegree.
- Perform topological sort from all the terminal nodes.

```cpp
class Solution {
public:
    vector<int> eventualSafeNodes(vector<vector<int>>& graph) {
        vector<int> safeNodes;
        vector<vector<int>> adj(graph.size());
        vector<int> indegree(graph.size());
        queue<int> q;
		
        // Reversing edges & counting indegree
        for(int i = 0; i < graph.size(); i++) {
            for(auto it: graph[i]) {
                adj[it].push_back(i);
                indegree[i]++;
            }
        }
		
        // Adding terminal nodes to queue
        for(int i = 0; i < indegree.size(); i++) {
            if(indegree[i] == 0) {
                q.push(i);
            }
        }
		
        while(!q.empty()) {
            int node = q.front();
            q.pop();
			
            safeNodes.push_back(node);
			
            for(auto it: adj[node]) {
                indegree[it]--;
				
                if(indegree[it] == 0) {
                    q.push(it);
                }
            }
        }
		
        sort(safeNodes.begin(), safeNodes.end());
		
        return safeNodes;   
    }
};
```

|   **Time Complexity**   | **Space Complexity** |
| :---------------------: | :------------------: |
| $O(N \log N + 3N + 2E)$ |     $O(4N + E)$      |





# References