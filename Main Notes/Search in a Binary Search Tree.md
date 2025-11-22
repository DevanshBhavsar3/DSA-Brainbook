02-11-2025  15:12

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Search in a Binary Search Tree

https://leetcode.com/problems/search-in-a-binary-search-tree/

- Iterate until root is null or root is the val.
- If the root's val is > val, move left.
- Else move right.

```cpp
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        while(root && root->val != val) {
            root = root->val > val ? root->left : root->right;
        }
		
        return root;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|     $O(\log N)$     |        $O(1)$        |





# References