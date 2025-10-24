20-10-2025  15:55

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Diameter of Binary Tree

https://leetcode.com/problems/diameter-of-binary-tree/

### Brute Force

- For every node get the left and right subtree height.
- Return the maximum addition of the left and right heights.

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
	
    int find(TreeNode* root, int maxi) {
        if(root == NULL) {
            return maxi;
        }
		
        int lh = getHeight(root->left);
        int rh = getHeight(root->right);
		
        maxi = max(maxi, lh + rh);
		
        return max(find(root->left, maxi), find(root->right, maxi));
    }
	
    int diameterOfBinaryTree(TreeNode* root) {
        return find(root, 0);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(N)$        |


### Optimal

- Find the height of the tree.
- And keep a max diameter variable which updates to the node's lh + rh.

```cpp
class Solution {
public:
    int getHeight(TreeNode* root, int& maxi) {
        if(root == NULL) {
            return 0;
        }
		
        int l = getHeight(root->left, maxi);
        int r = getHeight(root->right, maxi);
		
        maxi = max(maxi, l + r);
		
        return 1 + max(l, r);
    }
	
    int diameterOfBinaryTree(TreeNode* root) {
        int maxi = 0;
        int h = getHeight(root, maxi);
		
        return maxi;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References

[[Height of a Binary Tree]]