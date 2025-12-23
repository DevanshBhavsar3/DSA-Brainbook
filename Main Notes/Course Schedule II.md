23-12-2025  20:08

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Course Schedule II

https://leetcode.com/problems/course-schedule-ii/

- Imagine prerequisites as directed edge between courses, and perform topo sort. 
- If topo sort processed all the nodes, then return ans, else empty array.

```cpp
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses);
        vector<int> indegree(numCourses);
        vector<int> ans;
        queue<int> q;
		
        for(int i = 0; i < prerequisites.size(); i++) {
            adj[prerequisites[i][1]].push_back(prerequisites[i][0]);
            indegree[prerequisites[i][0]]++;
        }
		
        for(int i = 0; i < indegree.size(); i++) {
            if(indegree[i] == 0) {
                q.push(i);
            }
        }
		
        while(!q.empty()) {
            int node = q.front();
            q.pop();
			
            ans.push_back(node);
			
            for(auto it: adj[node]) {
                indegree[it]--;
				
                if(indegree[it] == 0) {
                    q.push(it);
                }
            }
        }
		
        if(ans.size() != numCourses) {
            return {};
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(2N + E)$     |       $O(3N)$        |
Excluding Adjacency List





# References
[[Topo Sort]]