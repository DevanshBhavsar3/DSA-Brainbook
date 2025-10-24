18-10-2025  12:57

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Recursive Preorder Traversal

https://leetcode.com/problems/binary-tree-preorder-traversal/

```cpp
class Solution {
public:
    void traverse(TreeNode* root, vector<int>& ans) {
        if(root == NULL) {
            return;
        }
        
        ans.push_back(root->val);
        
        traverse(root->left, ans);
        traverse(root->right, ans);
    }
    
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        
        traverse(root, ans);
        
        return ans;
    }
};
```

| **Time Complexity** |         **Space Complexity**          |
| :-----------------: | :-----------------------------------: |
|       $O(N)$        | $O(N)$, skewed tree in the worst case |





# References

[[Traversal Techniques]]