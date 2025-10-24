24-10-2025  14:00

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Vertical Order Traversal of BT

https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/

```cpp
class Solution {
public:
    void traverse(TreeNode* root, int row, int col, map<int, map<int, multiset<int>>>& nodes) {
        if(root == NULL) {
            return;
        }
		
        nodes[col][row].insert(root->val);
		
        traverse(root->left, row + 1, col - 1, nodes);
        traverse(root->right, row + 1, col + 1, nodes);
    }
	
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        vector<vector<int>> ans;
        map<int, map<int, multiset<int>>> nodes;
		
        traverse(root, 0, 0, nodes);
		
        for(auto v: nodes) {
            vector<int> level;
			
            for(auto l: v.second) {
                level.insert(level.end(), l.second.begin(), l.second.end());
            }
			
            ans.push_back(level);
        }
		
        return ans;
    }
};
```

| **Time Complexity** |    **Space Complexity**     |
| :-----------------: | :-------------------------: |
|    $O(N \log n)$    | $O(N) + O(N)$ (stack space) |





# References