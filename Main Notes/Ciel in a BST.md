03-11-2025  15:21

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Ciel in a BST

https://www.naukri.com/code360/problems/ceil-from-bst_920464

- If the curr == x, return curr.
- Else if curr > x, store curr and move to left.
- Else move to right.

```cpp
int findCeil(BinaryTreeNode<int> *node, int x){
    BinaryTreeNode<int>* curr = node;
    int ceil = -1;
	
    while(curr) {
        if(curr->data == x) {
            return curr->data;
        } else if(curr->data > x) {
            ceil = curr->data;
            curr = curr->left;
        } else {
            curr = curr->right;
        }
    }
	
    return ceil;
}
```

|      **Time Complexity**       | **Space Complexity** |
| :----------------------------: | :------------------: |
| $O(h)$, h = height of the tree |        $O(1)$        |





# References