01-11-2025  14:56

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Morris Traversal

### Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/

- Create a Threaded Binary Tree.
- Start from the root.
- If there is some left node,
	- Point the right-most node on the left subtree to curr and move left. (because you will end up at the right most node after the entire left subtree traversal).
	- If the right most node is already pointing to curr, cut the thread, add to the ans and move to right.
- Else add the node to ans and move right.

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        TreeNode* curr = root;
		
        while(curr) {
            if(curr->left == NULL) {
                ans.push_back(curr->val);
                curr = curr->right;
            } else {
                TreeNode* prev = curr->left;
				
				// O(N) for entire tree
				// Go to right most node
                while(prev->right && prev->right != curr) {
                    prev = prev->right;
                }
				
				// Point to curr
                if(prev->right == NULL) {
                    prev->right = curr;
                    curr = curr->left;
                } else {
	                // Remove pointer
                    prev->right = NULL;
                    ans.push_back(curr->val);
                    curr = curr->right;
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


### Preorder Traversal

https://leetcode.com/problems/binary-tree-preorder-traversal/

- Create a Threaded Binary Tree.
- Start from the root.
- If there is some left node,
	- Point the right-most node on the left subtree to curr, add curr to ans and move left. (because you will end up at the right most node after the entire left subtree traversal).
	- If the right most node is already pointing to curr, cut the thread and move to right.
- Else add the node to ans and move right.

```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        TreeNode* curr = root;
		
        while(curr) {
            if(curr->left == NULL) {
                ans.push_back(curr->val);
                curr = curr->right;
            } else {
                TreeNode* prev = curr->left;
				
				// O(N) for entire tree
                while(prev->right && prev->right != curr) {
                    prev = prev->right;
                }
				
                if(prev->right == NULL) {
                    prev->right = curr;
                    ans.push_back(curr->val);
                    curr = curr->left;
                } else {
                    prev->right = NULL;
                    curr = curr->right;
                }
            }
        }
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(1)$        |





# References