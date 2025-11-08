27-10-2025  16:16

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Binary Tree Paths

https://leetcode.com/problems/binary-tree-paths/

- Traverse the tree while adding the path to a container.
- When both left and right node are null add the container to the ans.

```cpp
class Solution {
public:
    void traverse(TreeNode* root, string container, vector<string>& ans) {
        if(!root->left && !root->right) {
            ans.push_back(container);
        }   
		
        if(root->left) {
            traverse(root->left, container + "->" + to_string(root->left->val), ans);
        }
		
        if(root->right) {
            traverse(root->right, container + "->" + to_string(root->right->val), ans);
        }
    }
	
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> ans;
        if(!root) {
            return ans;
        }
		
        traverse(root, to_string(root->val), ans);
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References