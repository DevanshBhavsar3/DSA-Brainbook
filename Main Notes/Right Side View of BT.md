26-10-2025  12:36

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Right Side View of BT

https://leetcode.com/problems/binary-tree-right-side-view/

- Perform reverse preorder traversal ( Root, Right, Left ).
- If the vector's size is same as the level add the node to the ans.

```cpp
class Solution {
public:
    void traverse(TreeNode* root, int row, vector<int>& ans) {
        if(root == NULL) {
            return;
        }
        if(row == ans.size()) {
            ans.push_back(root->val);            
        }
		
        traverse(root->right, row + 1, ans);
		
        traverse(root->left, row + 1, ans);
    }
	
    vector<int> rightSideView(TreeNode* root) {
        vector<int> ans;
		
        traverse(root, 0, ans);
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References