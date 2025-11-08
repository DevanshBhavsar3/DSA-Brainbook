31-10-2025  15:26

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Construct Binary Tree from Inorder and Postorder Traversal

https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/

![[Pasted image 20251031154430.png]]

- Hash the inorder elements with its index.
- The last element of the postorder will be the root.
- Find the it in the inorder,
	- The left elements will be of left subtree.
	- The right elements will be of right subtree.
- In the postorder, the no. of elements on the left from the inorder's root will be of the postorder's left subtree and same for the right.

```cpp
class Solution {
public:
    TreeNode* generate(vector<int>& inorder, int inStart, int inEnd, vector<int>& postorder, int postStart, int postEnd, map<int, int>& mp) {
        if(inStart > inEnd || postStart > postEnd) {
            return NULL;
        }
		
        TreeNode* root = new TreeNode(postorder[postEnd]);
		
        int inRoot = mp[postorder[postEnd]];
        int leftSize = inRoot - inStart;
		
        root->left = generate(inorder, inStart, inRoot - 1,
                            postorder, postStart, postStart + leftSize - 1, mp);
		
        root->right = generate(inorder, inRoot + 1, inEnd,
                            postorder, postStart + leftSize, postEnd - 1, mp);
                            
        return root;
    }
	
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        map<int, int> mp;
		
        for(int i = 0; i < inorder.size(); i++) {
            mp[inorder[i]] = i;
        }
		
        return generate(inorder, 0, inorder.size() - 1, postorder, 0, postorder.size() - 1, mp);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(2N)$        |





# References