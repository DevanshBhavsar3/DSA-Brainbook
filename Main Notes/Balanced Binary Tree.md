20-10-2025  15:28

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Balanced Binary Tree

https://leetcode.com/problems/balanced-binary-tree/

### Brute Force

- Recursively go to every node and find its left and right subtrees heights.
- If the difference is > 1, return false.
- Else call the function for left and right subtrees 

```cpp
class Solution {
public:
    int getHeight(TreeNode* root) {
        if(root == NULL) {
            return 0;
        }
		
        int l = getHeight(root->left);
        int r = getHeight(root->right);
		
        return 1 + max(l, r);
    }
	
    bool isBalanced(TreeNode* root) {
        if(root == NULL) {
            return true;
        }
		
        int l = getHeight(root->left);
        int r = getHeight(root->right);
		
        if(abs(l - r) > 1) {
            return false;
        }
		
        return isBalanced(root->left) && isBalanced(root->right);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(N)$        |


### Optimal

- Find the height of the binary tree.
- If the difference between the height of left and right subtree is > 1, return -1.
- If any of the height is -1, return -1.
- Finally if the recursion returned -1, return false else true.

```cpp
class Solution {
public:
    int getHeight(TreeNode* root) {
        if(root == NULL) {
            return 0;
        }
		
        int l = getHeight(root->left);
        if(l == -1) {
            return -1;
        }
		
        int r = getHeight(root->right);
        if(r == -1) {
            return -1;
        }
		
        if(abs(l - r) > 1) {
            return -1;
        }
		
        return 1 + max(l, r);
    }
	
    bool isBalanced(TreeNode* root) {
        int h = getHeight(root);
		
        if(h == -1) {
            return false;
        }
		
        return true;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References

[[Height of a Binary Tree]]