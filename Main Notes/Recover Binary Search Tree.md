09-11-2025  14:50

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Recover Binary Search Tree

https://leetcode.com/problems/recover-binary-search-tree/

### Brute Force

- Get the inorder traversal of the tree, and sort it.
- Change the node's value to its corresponding inorder idx.

```cpp
class Solution {
public:
    void getInorder(TreeNode* root, vector<int>& inorder) {
        if(root == NULL) {
            return;
        }
		
        getInorder(root->left, inorder);
        inorder.push_back(root->val);
        getInorder(root->right, inorder);
    }
	
    void convert(TreeNode* root, vector<int>& inorder, int& idx) {
        if(root == NULL || idx >= inorder.size()) {
            return;
        }
		
        convert(root->left, inorder, idx);
        
        root->val = inorder[idx];
        idx++;
		
        convert(root->right, inorder, idx);
    }
	
    void recoverTree(TreeNode* root) {
        vector<int> inorder;
		
        getInorder(root, inorder);
		
        sort(inorder.begin(), inorder.end());
		
        int idx = 0;
        convert(root, inorder, idx);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(2N + N \log N)$  |       $O(3N)$        |


### Optimal

- There can be only 2 possible violation cases,
	1. Both the incorrect node are adjacent in the inorder traversal.
	2. Both the incorrect node are not adjacent in the inorder traversal.
- Perform inorder traversal and whenever the node's val is not > its prev,
	- If first is NULL, store the root in the mid and prev in first.
	- Else store in last.
- At the end, if there is first and last, swap them.
- Else if first and mid (Adjacent case), swap them.

```cpp
class Solution {
public:
    TreeNode* first = NULL;
    TreeNode* mid = NULL;
    TreeNode* last = NULL;
    TreeNode* prev = NULL;
	
    void recover(TreeNode* root) {
        if(root == NULL) {
            return;
        }
		
        recover(root->left);
		
        if(prev && root->val < prev->val) {
            if(!first) {
                first = prev;
                mid = root;
            } else {
                last = root;
            }
        }
		
        prev = root;
		
        recover(root->right);
    }
	
    void recoverTree(TreeNode* root) {
        recover(root);
		
        if(first && last) {
            swap(first->val, last->val);
        } else if(first && mid) {
            swap(first->val, mid->val);
        }
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References