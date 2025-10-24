17-10-2025  12:33

Status:

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Introduction to Binary Trees

Binary trees is a **hierarchical data structure** used to represent data in a tree like structure with **at most 2** child for each of the parent node. 

Important definitions:
- The topmost node is known as **root** of the tree, and the later nodes are known as **children**.
- The node which doesn't have children is known as **leaf node**.
- The tree forming with the current node as root node is known as **sub-tree**.
- All the parent nodes of the current node is known as **Ancestors**.

![[image4QX4V9J.webp]]


## Types of Binary Trees

### Full BT

Each node either have 0 or 2 children.
 
![[Pasted image 20251017124602.jpg]]


### Complete BT

1. All levels are completely filled (have all the children nodes) except the last one.
2. The last level has all nodes as left as possible.

![[Pasted image 20251017124904.jpg]]


### Perfect BT

All leaf nodes are at the same level.

![[Pasted image 20251017125106.png]]


### Balanced BT

Height of the tree should be at most $\log(n)$. (n = no. of nodes)


### Degenerate Tree

Each node has only 1 child node.

![[Pasted image 20251017125641.jpg]]


## Representation in Code

```cpp
#include <bits/stdc++.h>

struct Node {
  int data;
  Node* left;
  Node* right;

  Node(int data) {
    this->data = data;
    left = right = NULL;
  }
};

int main(void) {
  Node* root = new Node(1);

  root->left = new Node(2);
  root->right = new Node(3);

  root->left->right = new Node(4);
}
```





# References