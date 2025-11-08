27-10-2025  16:19

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# LCA of Binary Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

### Brute Force

- Get the path from the root for both p and q.
- Find the last common node from both of the path and return it.

```cpp
class Solution {
public:
    bool getPath(TreeNode* root, TreeNode* x, vector<TreeNode*>& path) {
        if(root == NULL) {
            return false;
        }
		
        path.push_back(root);
		
        if(root->val == x->val) {
            return true;
        }
		
        if(getPath(root->left, x, path) ||
        getPath(root->right, x, path)) {
            return true;
        }
		
        path.pop_back();
		
        return false;
    }
	
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        vector<TreeNode*> pPath;
        vector<TreeNode*> qPath;
		
        getPath(root, p, pPath);
        getPath(root, q, qPath);
		
        int i = 0;
        while(i < pPath.size() && i < qPath.size() && pPath[i]->val == qPath[i]->val) {
            i++;
        }
		
        return pPath[i - 1];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(3N)$       |       $O(3N)$        |


### Optimal

- Traverse the tree and if you find a node that is either p or q, return it.
- If both left and right return some value, that means it is the lca, so return the current node.
- Else return the non-null node.

```cpp
class Solution {
public:
    TreeNode* traverse(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL || root == p || root == q) {
            return root;
        }
		
        TreeNode* left = traverse(root->left, p, q);
        TreeNode* right = traverse(root->right, p, q);
		
        if(left && right) {
            return root;
        } else if(left) {
            return left;
        } else {
            return right;
        }
    }
	
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        return traverse(root, p, q);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References