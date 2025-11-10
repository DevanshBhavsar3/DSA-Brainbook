18-10-2025  13:09

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Recursive Postorder Traversal

https://leetcode.com/problems/binary-tree-postorder-traversal/

```cpp
class Solution {
public:
    void traverse(TreeNode* root, vector<int>& ans) {
        if(root == NULL) {
            return;
        }
		
        traverse(root->left, ans);
        traverse(root->right, ans);
        ans.push_back(root->val);
    }
	
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
		
        traverse(root, ans);
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References

[[Traversal Techniques]]