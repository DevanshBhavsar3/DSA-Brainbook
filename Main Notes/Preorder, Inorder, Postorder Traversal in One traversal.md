19-10-2025  16:00

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Preorder, Inorder, Postorder Traversal in One traversal

https://www.naukri.com/code360/problems/tree-traversal_981269

- Add the node and its occurrence number in stack.
- If n is 1, add the node to preorder increase the n and add its left node to stack.
- If n is 2, add the node to inorder increase the n and add its right node to stack.
- Else, add the node to postorder.

```cpp
vector<vector<int>> getTreeTraversal(TreeNode *root){
    vector<vector<int>> ans(3);
	
    stack<pair<TreeNode*, int>> st;
    st.push({root, 1});
	
    while(!st.empty()) {
        pair<TreeNode*, int> top = st.top();
        st.pop();
		
        TreeNode* node = top.first;
        int n = top.second;
		
        if(n == 1) {
            ans[1].push_back(node->data);
            st.push({node, n + 1});
			
            if(node->left) {
                st.push({node->left, 1});
            }
        } else if(n == 2) {
            ans[0].push_back(node->data);
            st.push({node, n + 1});
			
            if(node->right) {
                st.push({node->right, 1});
            }
        } else {
            ans[2].push_back(node->data);
        }
    }
	
    return ans;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(3N)$       |       $O(4N)$        |





# References

[[Traversal Techniques]]