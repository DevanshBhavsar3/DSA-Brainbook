23-12-2025  19:49

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Course Schedule I

https://leetcode.com/problems/course-schedule/

- Imagine prerequisites as directed edge between courses, and perform topo sort. 
- If topo sort processed all the nodes, then return true, else false.

```cpp
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses);
        vector<int> indegree(numCourses);
        queue<int> q;
        int cnt = 0;
		
        for(int i = 0; i < prerequisites.size(); i++) {
            int u = prerequisites[i][0];
            int v = prerequisites[i][1];
			
            adj[v].push_back(u);
            indegree[u]++;
        }
		
        for(int i = 0; i < indegree.size(); i++) {
            if(indegree[i] == 0) {
                q.push(i);
            }
        }
		
        while(!q.empty()) {
            int node = q.front();
            q.pop();
			
            cnt++;
			
            for(auto it: adj[node]) {
                indegree[it]--;
				
                if(indegree[it] == 0) {
                    q.push(it);
                }
            }
        }
		
        return cnt == numCourses;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(2N + E)$     |       $O(2N)$        |
Excluding Adjacency List





# References
[[Topo Sort]]