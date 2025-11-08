08-11-2025  12:52

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Binary Search Tree Iterator

https://leetcode.com/problems/binary-search-tree-iterator/

### Brute Force

- Store the inorder traversal in vector.
- Keep a pointer to return the next node.

```cpp
class BSTIterator {
public:
    vector<int> inorder;
    int idx;
	
    BSTIterator(TreeNode* root) {
        generate(root, inorder);
        idx = 0;
    }
	
    void generate(TreeNode* root, vector<int>& inorder) {
        if(root == NULL) {
            return;
        }
		
        generate(root->left, inorder);
        inorder.push_back(root->val);
        generate(root->right, inorder);
    }
    
    int next() {
        return inorder[idx++];
    }
    
    bool hasNext() {
        return idx < inorder.size();
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(1)$        |        $O(N)$        |


### Optimal

- Perform iterative inorder traversal.
- First push all the left element to the stack.
- Whenever next() is called push all the left elements of the right subtree.

```cpp
class BSTIterator {
public:
    stack<TreeNode*> st;
	
    BSTIterator(TreeNode* root) {
        TreeNode* curr = root;
        pushAll(root);
    }
    
    int next() {
        TreeNode* node = st.top();
        st.pop();
		
        pushAll(node->right);
        
        return node->val;
    }
    
    bool hasNext() {
        return !st.empty();
    }
	
    void pushAll(TreeNode* root) {
        while(root) {
            st.push(root);
            root = root->left;
        }
    }
};
```

|                **Time Complexity**                 | **Space Complexity** |
| :------------------------------------------------: | :------------------: |
| $O(1)$ <br>O(total node push / total next() calls) |        $O(H)$        |





# References