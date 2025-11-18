01-11-2025  15:56

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Flatten Binary Tree to Linked List

https://leetcode.com/problems/flatten-binary-tree-to-linked-list/

### Better
#### Recursive

- Recurse in Right, Left, Root manner.
- Keep a prev pointer to which the curr node's right will point.

```cpp
class Solution {
public:
    TreeNode* prev = NULL;
	
    void flatten(TreeNode* root) {
        if(root == NULL) {
            return;
        }
		
        flatten(root->right);
        flatten(root->left);
		
        root->right = prev;
        root->left = NULL;
		
        prev = root;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |

#### Iterative

- Use a stack to connect nodes.
- Push left and right nodes to stack.
- Connect the stack's top to curr's right.

```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        if(root == NULL) {
            return;
        }
		
        stack<TreeNode*> st;
		
        st.push(root);
		
        while(!st.empty()) {
            TreeNode* node = st.top();
            st.pop();
			
            if(node->right) {
                st.push(node->right);
            }
			
            if(node->left) {
                st.push(node->left);
            }
			
            if(!st.empty()) {
                node->right = st.top();
            }
			
            node->left = NULL;
        }
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |


### Optimal

- Use morris traversal.
- If there is left, go to the right most node on the left subtree and connect its right to curr's right.
- Point curr's right to curr's left and curr's left to NULL.

```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        TreeNode* curr = root;
		
        while(curr) {
            if(curr->left) {
                TreeNode* prev = curr->left;
				
                while(prev->right) {
                    prev = prev->right;
                }
				
                prev->right = curr->right;
                curr->right = curr->left;
                curr->left = NULL;
            }
			
            curr = curr->right;
        }
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(1)$        |





# References