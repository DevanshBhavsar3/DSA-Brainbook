29-10-2025  16:44

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Minimum Time To Burn Binary Tree

https://www.naukri.com/code360/problems/time-to-burn-tree_1469067

- Map each node to its parent node.
- Start bfs from the start node until all the nodes are burnt.
- Insert the left, right and top nodes if they are not visited into the queue.
- Only increase time if you burn an adjacent node.

```cpp
#include <bits/stdc++.h>

// O(N)
BinaryTreeNode<int>* getParents(BinaryTreeNode<int>* root, map<BinaryTreeNode<int>*, BinaryTreeNode<int>*>& mp, int start) {
    queue<BinaryTreeNode<int>*> q;
    BinaryTreeNode<int>* startNode;
		
    q.push(root);
		
    while(!q.empty()) {
        BinaryTreeNode<int>* node = q.front();
        q.pop();
		
        if(node->data == start) {
            startNode = node;
        }
		
        if(node->left) {
            mp[node->left] = node;
            q.push(node->left);
        }
		
        if(node->right) {
            mp[node->right] = node;
            q.push(node->right);
        }
    }
	
    return startNode;
}

int timeToBurnTree(BinaryTreeNode<int>* root, int start)
{
    if(root == NULL) {
        return {};
    }
		
    map<BinaryTreeNode<int>*, BinaryTreeNode<int>*> parent;
    BinaryTreeNode<int>* startNode = getParents(root, parent, start);
		
    map<BinaryTreeNode<int>*, bool> visited;
    queue<BinaryTreeNode<int>*> q;
    int time = 0;
	
    q.push(startNode);
    visited[startNode] = true;
		
	// O(N)
    while(!q.empty()) {
        int size = q.size();
        int burnFlag = 0;
		
        for(int i = 0; i < size; i++) {
            BinaryTreeNode<int>* node = q.front();
            q.pop();
				
            if(node->left && !visited[node->left]) {
                burnFlag = 1;
                q.push(node->left);
                visited[node->left] = true;
            }
				
            if(node->right && !visited[node->right]) {
                burnFlag = 1;
                q.push(node->right);
                visited[node->right] = true;
            }
				
            if(parent[node] && !visited[parent[node]]) {
                burnFlag = 1;
                q.push(parent[node]);
                visited[parent[node]] = true;
            }
        }
		
        if(burnFlag) {
            time++;
        }
    }
	
    return time;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |       $O(3N)$        |





# References