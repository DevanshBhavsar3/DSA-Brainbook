23-11-2025  18:53

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# DFS in Graph

https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1

- For each node go to every connected node in the adjacency list is it is not visited.

```cpp
class Solution {
  public:
    void traverse(int i, vector<vector<int>>& adj, vector<int>& visited, vector<int>& ans) {
        ans.push_back(i);
        visited[i] = 1;
		
		// O(2E) overall
        for(auto it: adj[i]) {
            if(!visited[it]) {
                traverse(it, adj, visited, ans);
            }
        }
    }
  
    vector<int> dfs(vector<vector<int>>& adj) {
        vector<int> visited(adj.size());
        vector<int> ans;
        
        traverse(0, adj, visited, ans);
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O(N) + O(2E)$    |       $O(3N)$        |





# References