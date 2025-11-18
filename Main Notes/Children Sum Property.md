28-10-2025  19:40

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Children Sum Property

https://www.naukri.com/code360/problems/childrensumproperty_790723

- Get the sum of the child.
	- If it is >=, assign it to the root.
	- Else, assign root's value to both the child.
- Traverse on left and right.
- If the root is not leaf node assign the sum of both child to the root.

```cpp
void changeTree(BinaryTreeNode < int > * root) {
    if(root == NULL) {
        return;
    }
	
    int sum = 0;
	
    if(root->left) {
        sum += root->left->data;
    }
	
    if(root->right) {
        sum += root->right->data;
    }
	
    if(sum >= root->data) {
        root->data = sum;
    } else {
        if(root->left) {
            root->left->data = root->data;
        }
        
        if(root->right) {
            root->right->data = root->data;
        }
    }
	
    changeTree(root->left);
    changeTree(root->right);
	
    int total = 0;
	
    if(root->left) {
        total += root->left->data;
    }
	
    if(root->right) {
        total += root->right->data;
    }
	
    if(root->left || root->right) {
        root->data = total;
    }
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References