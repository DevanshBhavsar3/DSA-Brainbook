05-11-2025  16:17

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Kth Smallest Element in a BST

https://leetcode.com/problems/kth-smallest-element-in-a-bst/

### Better

- Create a sorted vector from the bst with inorder traversal.
- Return k - 1 element from the vector.

```cpp
class Solution {
public:
    void generateVector(TreeNode* root, vector<int>& elements) {
        if(root == NULL) {
            return;
        }
		
        generateVector(root->left, elements);
        elements.push_back(root->val);
        generateVector(root->right, elements);
    }
	
    int kthSmallest(TreeNode* root, int k) {
        vector<int> elements;
		
        generateVector(root, elements);
		
        return elements[k - 1];
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(2N)$        |


### Optimal

- Do morris inorder traversal with cnt variable.
- When the cnt is k - 1, return the node's val.

```cpp
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        TreeNode* curr = root;
        int cnt = 0;
        int ans = -1;
        while(curr) {
            if(cnt == k - 1) {
                ans = curr->val;
            }
			
            if(curr->left == NULL) {
                curr = curr->right;
                cnt++;
            } else {
                TreeNode* prev = curr->left;
				
                while(prev->right && prev->right != curr) {
                    prev = prev->right;
                }
				
                if(prev->right == NULL) {
                    prev->right = curr;
                    curr = curr->left;
                } else {
                    cnt++;
					
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
|       $O(N)$        |        $O(1)$        |


#### Kth Largest Element

- Count total nodes in the bst.
- Just find the n - kth smallest element.

or 

- Traverse in Right Root Left and return kth element.





# References

[[Morris Traversal]]