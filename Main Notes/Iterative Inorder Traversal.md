19-10-2025  12:52

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Iterative Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/

- Create a current node variable.
- If the curr_node != NULL, add it to the stack and move to the left.
- Else get the stack's top, add it to the ans and move to the right.

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        stack<TreeNode*> st;
		
        TreeNode* prev = root;
        
        while(prev != NULL || !st.empty()) {
            if(prev != NULL) {
                st.push(prev);
				
                prev = prev->left;
            } else {
                TreeNode* node = st.top();
                st.pop();
				
                ans.push_back(node->val);
				
                prev = node->right;
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

[[Recursive Inorder Traversal]]
[[Traversal Techniques]]