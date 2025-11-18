26-10-2025  13:00

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Symmetric Tree

https://leetcode.com/problems/symmetric-tree/

- Just check them like 2 seperate tree.
- Check left tree's left with right tree's right and similarly. (Mirror)

```cpp
class Solution {
public:
    bool check(TreeNode* left, TreeNode* right) {
        if(!left || !right) {
            return left == right;
        }
		
        if(left->val != right->val) {
            return false;
        }
		
        return check(left->left, right->right) && check(left->right, right->left);
    }
	
    bool isSymmetric(TreeNode* root) {
        return check(root->left, root->right);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |


### Iterative Approach

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        queue<TreeNode*> q;
		
        q.push(root->left);
        q.push(root->right);
		
        while(!q.empty()) {
            TreeNode* leftNode = q.front();
            q.pop();
			
            TreeNode* rightNode = q.front();
            q.pop();
			
            if(!leftNode && !rightNode) {
                continue;
            }
			
            if(!leftNode || !rightNode || leftNode->val != rightNode->val) {
                return false;
            }
			
            q.push(leftNode->left);
            q.push(rightNode->right);
            q.push(leftNode->right);
            q.push(rightNode->left);
        }
		
        return true;
    }
};
```





# References