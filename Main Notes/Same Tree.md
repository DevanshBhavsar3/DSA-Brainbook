21-10-2025  16:17

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Same Tree

https://leetcode.com/problems/same-tree/

- Perform any traversal and ensure both the tree generate same sequence. 

```cpp
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p == NULL || q == NULL) {
            return p == q;
        }
		
        if(p->val != q->val) {
            return false;
        }
		
        return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References

[[Traversal Techniques]]