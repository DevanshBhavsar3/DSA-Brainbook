07-11-2025  14:43

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Construct BST from Preorder Traversal

https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/

### Brute Force

 - For every element in the preorder array, find its position in the tree.
 - If the position is NULL, create a new node with that element.

```cpp
class Solution {
public:
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        if(preorder.size() <= 0) {
            return NULL;
        }
		
        TreeNode* root = new TreeNode(preorder[0]);
		
        for(int i = 1; i < preorder.size(); i++) {
            TreeNode* curr = root;
			
            while(true) {
                if(preorder[i] < curr->val) {
                    if(!curr->left) {
                        curr->left = new TreeNode(preorder[i]);
                        break;
                    }
					
                    curr = curr->left;
                } else {
                    if(!curr->right) {
                        curr->right = new TreeNode(preorder[i]);
                        break;
                    }
					
                    curr = curr->right;
                }
            }
        }
		
        return root;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(1)$        |


### Better

- The inorder of the bst is always sorted.
- So, get the inorder by sorting the preorder and construct bst from them.

```cpp
class Solution {
public:
    TreeNode* generate(vector<int>& preorder, int preStart, int preEnd, vector<int>& inorder, int inStart, int inEnd, map<int, int>& mp) {
        if(preStart > preEnd || inStart > inEnd) {
            return NULL;
        }
		
        TreeNode* root = new TreeNode(preorder[preStart]);
        int inRoot = mp[preorder[preStart]];
        int size = inRoot - inStart;
		
        root->left = generate(
            preorder, preStart + 1, preStart + size,
            inorder, inStart, inRoot - 1,
            mp);
		
        root->right = generate(
            preorder, preStart + size + 1, preEnd,
            inorder, inRoot + 1, inEnd,
            mp);
		
        return root;
    }
	
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        vector<int> inorder(preorder);
        map<int, int> mp;
		
        sort(inorder.begin(), inorder.end());
		
        for(int i = 0; i < inorder.size(); i++) {
            mp[inorder[i]] = i;
        }
		
        return generate(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1, mp);
    }
};
```

| **Time Complexity**  | **Space Complexity** |
| :------------------: | :------------------: |
| $O(N \log N) + O(N)$ |       $O(3N)$        |


### Optimal

- Maintain an upper bound.
- If the element is > ub, return NULL.
- Create new node and go to left and update ub to root's val.
- Also, go to right and pass the parent ub.

```cpp
class Solution {
public:
    TreeNode* generate(vector<int>& preorder, int& idx, int ub) {
        if(idx >= preorder.size() || preorder[idx] > ub) {
            return NULL;
        }
		
        TreeNode* root = new TreeNode(preorder[idx]);
        
        idx++;
        
        root->left = generate(preorder, idx, root->val);
        root->right = generate(preorder, idx, ub);
		
        return root;
    }
	
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        int idx = 0;
		
        return generate(preorder, idx, INT_MAX);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References

[[Construct BST from Preorder Traversal]]