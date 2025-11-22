09-11-2025  15:35

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Largest BST in BT

https://www.naukri.com/code360/problems/size-of-largest-bst-in-binary-tree_893103

### Brute Force

- Go to every node and validate if it is a valid BST.
- If it is valid BST, get its size.
- Return maximum size across the tree.

```cpp
bool validate(TreeNode* root, int low, int high, int& size) {
    if(root == NULL) {
        return true;
    }
	
    size++;
	
    if(root->data <= low || root->data >= high) {
        size = -1;
        return false;
    }
	
    return validate(root->left, low, root->data, size) && validate(root->right, root->data, high, size);
}

int getLargestBST(TreeNode* root) {
    if(root == NULL) {
        return 0;
    }
	
    int size = 0;
	
    validate(root, INT_MIN, INT_MAX, size);
	
    return max(size, max(getLargestBST(root->left), getLargestBST(root->right)));
}

int largestBST(TreeNode * root){
    return getLargestBST(root);
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |       $O(N^2)$       |


### Optimal

- Perform post order traversal.
- Get the largest value from left and smallest value from the right as well as the size.
- If the current node is > largest and < smallest, return them with size.
- Else return INT_MAX, INT_MIN, and maximum size.

```cpp
struct NodeValue {
    int largest;
    int smallest;
    int size;
	
    NodeValue(int l, int s, int si) {
        largest = l;
        smallest = s;
        size = si;
    }
};

NodeValue getLargest(TreeNode* root) {
    if(root == NULL) {
        return NodeValue(INT_MIN, INT_MAX, 0);
    }
	
    NodeValue left = getLargest(root->left);
    NodeValue right = getLargest(root->right);
	
    if(root->data > left.largest && root->data < right.smallest) {
        return NodeValue(max(root->data, right.largest), min(root->data, left.smallest), 1 + right.size + left.size);
    }
	
    return NodeValue(INT_MAX, INT_MIN, max(left.size, right.size));
}

int largestBST(TreeNode * root){
    return getLargest(root).size;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References