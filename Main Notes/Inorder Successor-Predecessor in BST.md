07-11-2025  15:49

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Inorder Successor-Predecessor in BST

https://www.naukri.com/code360/problems/predecessor-and-successor-in-bst_893049

### Brute Force

- Get the inorder traversal of the BST.
- Find the key in the traversal and return elements before and after the key.

```cpp
void getInorder(TreeNode* root, vector<int>& inorder) {
    if(root == NULL) {
        return;
    }
	
    getInorder(root->left, inorder);
    inorder.push_back(root->data);
    getInorder(root->right, inorder);
}

pair<int, int> predecessorSuccessor(TreeNode *root, int key)
{
    vector<int> inorder;
    getInorder(root, inorder);
	
    int low = 0;
    int high = inorder.size() - 1;
	
    if(inorder.size() == 1) {
        return {-1, -1};
    }
	
    while(low <= high) {
        int mid = low + (high - low) / 2;
		
        if(inorder[mid] == key) {
            int pred = mid - 1 >= 0 ? inorder[mid - 1] : -1;
            int succ = mid + 1 < inorder.size() ? inorder[mid + 1] : -1;
			
            return {pred, succ};
        } else if(inorder[mid] > key) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
	
    int pred = low - 1 >= 0 ? inorder[low - 1] : -1;
    int succ = low < inorder.size() ? inorder[low] : -1;
	
    return {pred, succ};
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
| $O(N) + O(\log N)$  |       $O(2N)$        |


### Better

- Perform inorder morris traversal until the node's value is > key.
- If the node's value < key, update the pred.

```cpp
pair<int, int> predecessorSuccessor(TreeNode *root, int key)
{
    int pred = -1;
    int succ = -1;
    TreeNode* curr = root;
	
    while(curr) {
        if(!curr->left) {
            if(curr->data > key) {
                succ = curr->data;
                break;
            }
			
            if(curr->data < key) {
                pred = curr->data;
            }
			
            curr = curr->right;
        } else {
            TreeNode* prev = curr->left;
			
            while(prev->right && prev->right != curr) {
                prev = prev->right;
            }
			
            if(!prev->right) {
                prev->right = curr;
                curr = curr->left;
            } else {
                prev->right = NULL;
				
                if(curr->data < key) {
                    pred = curr->data;
                }
				
                if(curr->data > key) {
                    succ = curr->data;
                    break;
                }
				
                curr = curr->right;
            }
        }
    }
    
    return {pred, succ};
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(1)$        |


### Optimal

 - Perform binary search on the bst.
 - For successor, if the curr node is <= key, go to right, else left while saving the node.
 - For predecessor, if the curr node is >= key, go to left, else right while saving the node.

```cpp
pair<int, int> predecessorSuccessor(TreeNode *root, int key)
{
    int succ = -1;
    TreeNode* curr = root;
	
    while(curr) {
        if(curr->data <= key) {
            curr = curr->right;
        } else {
            succ = curr->data;
            curr = curr->left;
        }
    }
	
    int pred = -1;
    curr = root;
	
    while(curr) {
        if(curr->data >= key) {
            curr = curr->left;
        } else {
            pred = curr->data;
            curr = curr->right;
        }
    }
	
    return {pred, succ};
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2H)$       |        $O(1)$        |





# References 