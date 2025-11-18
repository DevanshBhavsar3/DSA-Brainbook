29-10-2025  15:10

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# All Nodes at Distance K in Binary Tree

https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/

- Map every node to its parent node.
- Start bfs from the target node for k time.
- Insert the left, right and top nodes if they are not visited into the queue.

```cpp
class Solution {
public:
	// O(N)
    void getParents(TreeNode* root, map<TreeNode*, TreeNode*>& mp) {
        queue<TreeNode*> q;
		
        q.push(root);
		
        while(!q.empty()) {
            TreeNode* node = q.front();
            q.pop();
			
            if(node->left) {
                mp[node->left] = node;
                q.push(node->left);
            }
			
            if(node->right) {
                mp[node->right] = node;
                q.push(node->right);
            }
        }
    }
	
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        if(root == NULL) {
            return {};
        }
		
        map<TreeNode*, TreeNode*> parent;
        getParents(root, parent);
		
        map<TreeNode*, bool> visited;
        queue<TreeNode*> q;
        int dist = 0;
		
        q.push(target);
        visited[target] = true;
		
		// O(N)
        while(!q.empty()) {
            if(dist == k) {
                break;
            }
			
            int size = q.size();
            for(int i = 0; i < size; i++) {
                TreeNode* node = q.front();
                q.pop();
				
                if(node->left && !visited[node->left]) {
                    q.push(node->left);
                    visited[node->left] = true;
                }
				
                if(node->right && !visited[node->right]) {
                    q.push(node->right);
                    visited[node->right] = true;
                }
				
                if(parent[node] && !visited[parent[node]]) {
                    q.push(parent[node]);
                    visited[parent[node]] = true;
                }
            }
			
            dist++;
        }
		
        vector<int> ans;
		
        while(!q.empty()) {
            ans.push_back(q.front()->val);
            q.pop();
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |       $O(3N)$        |





# References