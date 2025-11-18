25-10-2025  14:40

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Bottom View of Binary Tree

https://www.naukri.com/code360/problems/bottom-view-of-binary-tree_893110

- Perform level order traversal with the vertical column no.
- Map the node to its vertical column no.
- Transfer data from map to vector and return.

```cpp
#include <bits/stdc++.h>

vector<int> bottomView(TreeNode<int> * root){
    queue<pair<TreeNode<int>*, int>> q;
    map<int, int> mp;
	
    q.push({root, 0});
	
    while(!q.empty()) {
        int size = q.size();
		
        for(int i = 0; i < size; i++) {
            auto node = q.front();
            q.pop();
			
            mp[node.second] = node.first->data;
			
            if(node.first->left) {
                q.push({node.first->left, node.second - 1});
            }
			
            if(node.first->right) {
                q.push({node.first->right, node.second + 1});
            }
        }
    }
	
    vector<int> ans;
	
    for(auto it: mp) {
        ans.push_back(it.second);
    }
	
    return ans;
}
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |       $O(2N)$        |





# References

[[Level Order Traversal]]
[[Vertical Order Traversal of BT]]