18-10-2025  13:00

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Recursive Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/

```cpp
class Solution {
public:
    void traverse(TreeNode* root, vector<int>& ans) {
        if(root == NULL) {
            return;
        }
        
        traverse(root->left, ans);
        ans.push_back(root->val);
        traverse(root->right, ans);
    }
    
    vector<int> inorderTraversal(TreeNode* root) {
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