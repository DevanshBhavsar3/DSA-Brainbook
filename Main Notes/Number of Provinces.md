24-11-2025  18:19

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Number of Provinces

https://leetcode.com/problems/number-of-provinces/

- Create a visited array.
- For every element in visited array, if it is not visited do any traversal.
- Count how many element was not visited after traversal.

```cpp
class Solution {
public:
    void traverse(int node, vector<vector<int>>& isConnected, vector<int>& visited) {
        visited[node] = 1;
		
        for(int i = 0; i < isConnected[node].size(); i++) {
            if(isConnected[node][i] && !visited[i]) {
                traverse(i, isConnected, visited);
            }
        }
    }
	
    int findCircleNum(vector<vector<int>>& isConnected) {   
        vector<int> visited(isConnected.size());
        int provinces = 0;
		
        for(int i = 0; i < visited.size(); i++) {
            if(!visited[i]) {
                provinces++;
                traverse(i, isConnected, visited);
            }
        }
		
        return provinces;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(N) + O(N^2)$<br> |       $O(2N)$        |





# References