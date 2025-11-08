02-11-2025  15:27

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Find Min-Max in BST

https://www.naukri.com/code360/problems/minimum-element-in-bst_8160462

- The left-most node will be the smallest element.
- The right-most node will be the biggest element.

```cpp
int minVal(Node* root){
	if(!root) {
		return -1;
	}
	
	while(root->left) {
		root = root->left;
	}
	
	return root->data;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References