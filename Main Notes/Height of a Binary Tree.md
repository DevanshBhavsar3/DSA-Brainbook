20-10-2025  15:16

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Height of a Binary Tree

https://leetcode.com/problems/maximum-depth-of-binary-tree/

- Return the the 1 + max(left, right) for every root. 

```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == NULL) {
            return 0;
        }
		
        int l = maxDepth(root->left);
        int r = maxDepth(root->right);
		
        return 1 + max(l, r);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References