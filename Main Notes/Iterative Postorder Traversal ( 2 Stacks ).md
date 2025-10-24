19-10-2025  13:29

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Iterative Postorder Traversal ( 2 Stacks )

https://leetcode.com/problems/binary-tree-postorder-traversal/

- Push root the stack 1.
- Add the top of the stack 1 to the stack 2 and add that node's left and right to stack 1.
- Move all the elements from stack 2 to array and return.

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        if(root == NULL) return {};
		
        stack<TreeNode*> st1;
        stack<TreeNode*> st2;
		
        st1.push(root);
		
        while(!st1.empty()) {
            TreeNode* node = st1.top();
            st1.pop();
			
            st2.push(node);
			
            if(node->left) {
                st1.push(node->left);
            }
			
            if(node->right) {
                st1.push(node->right);  
            }
        }
		
        vector<int> ans;
		
        while(!st2.empty()) {
            ans.push_back(st2.top()->val);
            st2.pop();
        }
		
        return ans;
    }
};
```

> First stack is doing preorder traversal: Root, Left, Right
> Pushing to stack 2 swaps right and left: Root, Right , Left
> Ans in the stack 2 is reversed: Left, Right, Root

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |       $O(2N)$        |





# References

[[Recursive Postorder Traversal]]
[[Traversal Techniques]]