05-11-2025  15:26

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Delete Node in a BST

https://leetcode.com/problems/delete-node-in-a-bst/

- Find the parent node of the key node.
- If there is not left of keyNode, point parent node to right node and vice-versa.
- Else, get the right most node from the left subtree and point it's right to the keynode's right.
- Point parent to keynode's left.
- If the root is the keyNode, call the helper function directly.

```cpp
class Solution {
public:
    TreeNode* findLastRight(TreeNode* root) {
        if(root->right == NULL) {
            return root;
        }
		
        return findLastRight(root->right);
    }
	
    TreeNode* helper(TreeNode* root) {
        if(root->left == NULL) {
            return root->right;
        } else if(root->right == NULL) {
            return root->left;
        }
		
        TreeNode* rightChild = root->right;
        TreeNode* lastRight = findLastRight(root->left);
		
        lastRight->right = rightChild;
		
        return root->left;
    }
	
    TreeNode* deleteNode(TreeNode* root, int key) {
        if(root == NULL) {
            return NULL;
        }
		
        if(root->val == key) {
            return helper(root);
        }
		
        TreeNode* curr = root;
		
        while(curr) {
            if(curr->val < key) {
                if(curr->right && curr->right->val == key) {
                    curr->right = helper(curr->right);
                    break;
                }
				
                curr = curr->right;
            } else {
                if(curr->left && curr->left->val == key) {
                    curr->left = helper(curr->left);
                    break;
                }
				
                curr = curr->left;
            }
        }
		
        return root;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(H)$        |        $O(1)$        |





# References