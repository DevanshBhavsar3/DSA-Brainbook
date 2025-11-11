21-10-2025  16:26

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Zigzag Traversal

https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/

- Perform the level order traversal with a flag for direction.
- If the flag is on add the value from last, else from front.
- Toggle the flag at every level.

```cpp
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> ans;
		
        if(root == NULL) {
            return ans;
        }
		
        queue<TreeNode*> q;
        int dir = 0;
		
        q.push(root);
		
        while(!q.empty()) {
            int size = q.size();
            vector<int> level(size);
			
            for(int i = 0; i < size; i++) {
                TreeNode* node = q.front();
                q.pop();
				
				
                int idx = dir ? size - 1 - i : i;
                level[idx] = node->val;
				
                if(node->left) {
                    q.push(node->left);
                }
				
                if(node->right) {
                    q.push(node->right);
                }
            }
			
            ans.push_back(level);
            dir ^= 1;
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References

[[Level Order Traversal]]