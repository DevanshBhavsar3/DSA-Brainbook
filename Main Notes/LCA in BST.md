06-11-2025  16:31

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# LCA in BST

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

[[LCA of Binary Tree]]

### Optimal

- If both p and q are on left, move left and vice-versa.
- Else one will be on the left and one will be on the right, so the curr node will be the LCA.
- Else curr node will be one of the p and q, and it will be the LCA.

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL) {
            return NULL;
        }
        
        if(p->val < root->val && q->val < root->val) {
            return lowestCommonAncestor(root->left, p, q);
        } else if(p->val > root->val && q->val > root->val) {
            return lowestCommonAncestor(root->right, p, q);
        } else {
            return root;
        }
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(H)$        |        $O(1)$        |





# References