24-10-2025  13:06

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Boundary Traversal of BT

https://www.naukri.com/code360/problems/boundary-traversal_790725

- Get all the nodes from the left boundary, if there is no left go to right.
- Traverse the tree and get only the leaf nodes.
- Get all the nodes from the right boundary in reverse order, if there is no right go to left.

```cpp
#include <bits/stdc++.h>

bool isLeaf(TreeNode<int>* root) {
    return !root->left && !root->right;
}

void addLeaves(TreeNode<int>* root, vector<int>& ans) {
    if(isLeaf(root)) {
        ans.push_back(root->data);
        return;
    }
	
    if(root->left) {
        addLeaves(root->left, ans);
    }
	
    if(root->right) {
        addLeaves(root->right, ans);
    }
}

vector<int> traverseBoundary(TreeNode<int> *root)
{
	vector<int> ans;
    if(root == NULL) return ans;
    
    if(!isLeaf(root)) {
        ans.push_back(root->data);
    }
 
    TreeNode<int>* curr = root->left;
	
    // Get left boundary nodes
    while(curr) {
        if(!isLeaf(curr)) {
            ans.push_back(curr->data);
        }
		
        if(curr->left) {
            curr = curr->left;
        } else {
            curr = curr->right;
        }
    }
	
    // Get the leaf nodes
    addLeaves(root, ans);
	
    stack<int> st; 
    curr = root->right;
	
    // Get right boundary nodes
    while(curr) {
        if(!isLeaf(curr)) {
            st.push(curr->data);
        }
		
        if(curr->right) {
            curr = curr->right;
        } else {
            curr = curr->left;
        }
    }
	
    while(!st.empty()) {
        ans.push_back(st.top());
        st.pop();
    }
	
    return ans;
}
```

| **Time Complexity**  | **Space Complexity** |
| :------------------: | :------------------: |
| $O(H) + O(H) + O(N)$ |        $O(N)$        |





# References