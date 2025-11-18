28-10-2025  18:19

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Maximum Width of Binary Tree

https://leetcode.com/problems/maximum-width-of-binary-tree/

- Perform level order traversal while assigning the hypothetical index to each node.
- The index of the node will be,
	- (Parent's index - min index on that level) $* 2 + 1$, for left.
	- (Parent's index - min index on that level) $*2 + 2$, for right.
- The width of the level will be last index - first index + 1.

```cpp
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        if(root == NULL) {
            return 0;
        }
		
        queue<pair<TreeNode*, int>> q;
        int maxi = INT_MIN;
		
        q.push({root, 0});
		
        while(!q.empty()) {
            int size = q.size();
            int mini = q.front().second;
            int first = 0;
            int last = 0;
			
            for(int i = 0; i < size; i++) {
                pair<TreeNode*, int> node = q.front();
                q.pop();
				
                int currIdx = node.second - mini;
				
                if(i == 0) {
                    first = currIdx;
                } else if(i == size - 1) {
                    last = currIdx;
                }
				
                if(node.first->left) {
                    q.push({node.first->left, (long) currIdx * 2 + 1});
                }
				
                if(node.first->right) {
                    q.push({node.first->right, (long) currIdx * 2 + 2});
                }
            }
			
            maxi = max(maxi, last - first + 1);
        }   
		
        return maxi;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References