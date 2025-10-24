18-10-2025  13:17

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Level Order Traversal

https://leetcode.com/problems/binary-tree-level-order-traversal/

- Create a queue with the root element initially.
- While the queue is not empty,
	- Get all the element from the queue.
	- Push their and right element to the queue.
	- Push the value in some container.
	- After iterating for all the element, add the container to ans.

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        queue<TreeNode*> qu;
        vector<vector<int>> ans;
		
        if(root == NULL) return ans;
		
        qu.push(root);
		
        while(!qu.empty()) {
            vector<int> container;
            int size = qu.size();
			
            for(int i = 0; i < size; i++) {
                TreeNode* node = qu.front();
                qu.pop();
				
                if(node->left) {
                    qu.push(node->left);
                }
				
                if(node->right) {
                    qu.push(node->right);
                }
				
                container.push_back(node->val);
            }
			
            ans.push_back(container);
        }
        
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |  $O(N)$, Queue size  |





# References

[[Traversal Techniques]]