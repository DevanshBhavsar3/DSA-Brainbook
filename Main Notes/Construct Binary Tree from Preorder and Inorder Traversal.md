31-10-2025  14:37

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Construct Binary Tree from Preorder and Inorder Traversal

https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

![[Pasted image 20251031151850.png]]

- Create a new root node which will be preorder's start.
- Find that values in inorder,
	- The left elements will be of left subtree.
	- All the right elements will be of right subtree.
- In preorder array the no. of elements on the left from the inorder's root will be of preorder's left subtree and same for the right.

```cpp
class Solution {
public:
    TreeNode* generate(vector<int>& preorder, int preStart, int preEnd, vector<int>& inorder, int inStart, int inEnd, map<int, int>& mp) {
        if(preStart > preEnd || inStart > inEnd) {
            return NULL;
        }
		
        TreeNode* root = new TreeNode(preorder[preStart]);
		
        int i = mp[preorder[preStart]];
        int leftSize = i - inStart;
		
        root->left = generate(preorder, preStart + 1, preStart + leftSize, 
                            inorder, inStart, i - 1, mp);
        root->right = generate(preorder, preStart + leftSize + 1, preEnd,
                            inorder, i + 1, inEnd, mp);
		
        return root;
    }
	
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        map<int, int> mp;
		
        for(int i = 0; i < inorder.size(); i++) {
            mp[inorder[i]] = i;
        }
        return generate(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1, mp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(2N)$        |





# References