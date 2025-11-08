03-11-2025  15:37

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Insert into a BST

https://leetcode.com/problems/insert-into-a-binary-search-tree/

- Traverse until the left or right is NULL.
- If it is NULL, add the new node at that position.

> The new node will always be the leaf node.

```cpp
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(root == NULL) {
            return new TreeNode(val);
        }
		
        TreeNode* curr = root;
		
        while(curr) {
            if(curr->val < val) {
                if(curr->right) {
                    curr = curr->right;
                } else {
                    curr->right = new TreeNode(val);
                    break;
                }
            } else {
                if(curr->left) {
                    curr = curr->left;
                } else {
                    curr->left = new TreeNode(val);
                    break;
                }
            }
        }
		
        return root;
    }
};
```

|      **Time Complexity**       | **Space Complexity** |
| :----------------------------: | :------------------: |
| $O(h)$, h = height of the tree |        $O(1)$        |





# References