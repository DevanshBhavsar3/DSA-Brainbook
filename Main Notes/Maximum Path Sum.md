21-10-2025  15:46

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Maximum Path Sum

https://leetcode.com/problems/binary-tree-maximum-path-sum/

- Calculate the sum of the nodes of left and right subtree.
- If the sum is < 0, change it to 0.
- Update the max to maximum path sum.
- Return the sum of path that is maximum.

```cpp
class Solution {
public:
    int getSum(TreeNode* root, int& maxi) {
        if(root == NULL) {
            return 0;
        }
		
        int ls = max(0, getSum(root->left, maxi));
        int rs = max(0, getSum(root->right, maxi));
		
        maxi = max(maxi, root->val + ls + rs);
		
        return root->val + max(ls, rs);
    }
	
    int maxPathSum(TreeNode* root) {
        int ans = INT_MIN;
		
        getSum(root, ans);
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References