30-10-2025  15:35

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Count Complete Tree Nodes

https://leetcode.com/problems/count-complete-tree-nodes/

### Brute Force

- Count nodes while traversing.

```cpp
class Solution {
public:
    int countNodes(TreeNode* root) {
        if(root == NULL) {
            return 0;
        }
		
        return 1 + countNodes(root->left) + countNodes(root->right);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |  $O(h), h = \log n$  |


### Optimal

- While traversing check if the left and right height of the subtree is same.
- If it is return $2^h - 1$.
- Else traverse further.

```cpp
class Solution {
public:
    int getLeftHeight(TreeNode* root) {
        TreeNode* curr = root;
        int h = 0;
		
        while(curr) {
            curr = curr->left;
            h++;
        }
		
        return h;
    }
	
    int getRightHeight(TreeNode* root) {
        TreeNode* curr = root;
        int h = 0;
		
        while(curr) {
            curr = curr->right;
            h++;
        }
		
        return h;
    }
	
    int countNodes(TreeNode* root) {
        if(root == NULL) {
            return 0;
        }
		
        int lh = getLeftHeight(root);
        int rh = getRightHeight(root);
		
        if(lh == rh) {
            return (1 << lh) - 1;
        }
		
        return 1 + countNodes(root->left) + countNodes(root->right);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|   $O((\log n)^2)$   |     $O(\log N)$      |

> $\log N$ for traversing in the worst case and another $\log N$ for finding the left and right height.





# References