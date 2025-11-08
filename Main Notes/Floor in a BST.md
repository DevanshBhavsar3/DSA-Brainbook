03-11-2025  15:30

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Floor in a BST

https://www.naukri.com/code360/problems/floor-from-bst_920457

- If the curr == x, return curr.
- Else if curr < x, store curr and move to right.
- Else, move to left.

```cpp
int floorInBST(TreeNode<int> * root, int X)
{
    TreeNode<int>* curr = root;
    int floor = -1;
	
    while(curr) {
        if(curr->val == X) {
            return curr->val;
        } else if(curr->val > X) {
            curr = curr->left;
        } else {
            floor = curr->val;
            curr = curr->right;
        }
    }
	
    return floor;
}
```

|      **Time Complexity**       | **Space Complexity** |
| :----------------------------: | :------------------: |
| $O(h)$, h = height of the tree |        $O(1)$        |





# References