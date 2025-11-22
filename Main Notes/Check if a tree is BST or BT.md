06-11-2025  15:53

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Check if a tree is BST or BT

https://leetcode.com/problems/validate-binary-search-tree/

- Create a range, with initial LONT_MIN and LONG_MAX.
- If the node's vale is out of the range, return false.
- When going left update high to curr node's value.
- When going right update low to curr node's value.

```cpp
class Solution {
public:
    bool check(TreeNode* root, long low, long high) {
        if(root == NULL) {
            return true;
        }
		
        if(root->val <= low || root->val >= high) {
            return false;
        }
		
        return check(root->left, low, root->val) && check(root->right, root->val, high);
    }
	
    bool isValidBST(TreeNode* root) {
        return check(root, LONG_MIN, LONG_MAX);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References