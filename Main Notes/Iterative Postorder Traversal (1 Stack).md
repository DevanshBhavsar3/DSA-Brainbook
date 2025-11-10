19-10-2025  15:10

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Iterative Postorder Traversal (1 Stack)

https://leetcode.com/problems/binary-tree-postorder-traversal/

- Go to the left as much as possible.
- If the left becomes null move to the right.
	- If the right is also null, add the parent (st.top) to the ans.
	- Also add all the ancestors(whose right sub-tree you just processed) of that node to the ans. 
	- Else move the curr pointer to the right.

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        stack<TreeNode*> st;
        vector<int> ans;
		
        if (root == NULL) return ans;
		
        TreeNode* curr = root;
		
        while (curr != NULL || !st.empty()) {
            if (curr) {
                st.push(curr);
				
                curr = curr->left;
            } else {
                TreeNode* tmp = st.top()->right;
				
                if (tmp == NULL) {
                    tmp = st.top();
                    st.pop();
					
                    ans.push_back(tmp->val);
					
                    while (!st.empty() && tmp == st.top()->right) {
                        tmp = st.top();
                        st.pop();
						
                        ans.push_back(tmp->val);
                    }
                } else {
                    curr = tmp;
                }
            }
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(N)$        |





# References

[[Iterative Postorder Traversal ( 2 Stacks )]]
[[Recursive Postorder Traversal]]
[[Traversal Techniques]]