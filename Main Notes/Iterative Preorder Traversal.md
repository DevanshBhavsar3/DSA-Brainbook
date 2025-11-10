19-10-2025  12:41

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Iterative Preorder Traversal

https://leetcode.com/problems/binary-tree-preorder-traversal/

```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        
        if(root == NULL) return ans;
		
        stack<TreeNode*> st;
        st.push(root);
		
        while(!st.empty()) {
            TreeNode* node = st.top();
            st.pop();
			
            ans.push_back(node->val);
			
            if(node->right) {
                st.push(node->right);
            }
			
            if(node->left) {
                st.push(node->left);
            }
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References

[[Recursive Preorder Traversal]]
[[Traversal Techniques]]