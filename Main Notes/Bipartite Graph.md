20-12-2025  19:04

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Bipartite Graph

https://leetcode.com/problems/is-graph-bipartite/

> Condition for bipartite:
> Every connected nodes are from different sets.

- Color every adjacent node with different color. (Hypothetically dividing them in sets)
- If you find a adjacent node that is colored with the same color (In the same set), then it can't be a bipartite graph.

```cpp
class Solution {
public:
    bool traverse(int node, int c, vector<vector<int>>& graph, vector<int>& color) {
        color[node] = c;
		
        for(auto it: graph[node]) {
            if(color[it] == -1) {
                if(traverse(it,  !c, graph, color) == false) {
                    return false;
                }
            } else if(color[it] == c) {
                return false;
            }
        }
		
        return true;
    }
	
    bool isBipartite(vector<vector<int>>& graph) {
        vector<int> color(graph.size(), -1);
		
        for(int i = 0; i < color.size(); i++) {
            if(color[i] == -1) {
				// Overall O(N + 2E)
                if(traverse(i, 0, graph, color) == false) {
                    return false;
                }
            }
        }
		
        return true;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(2N + 2E)$     |       $O(2N)$        |





# References