08-11-2025  13:22

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Search Trees]]

# Two Sum in BST

https://leetcode.com/problems/two-sum-iv-input-is-a-bst/

### Brute Force

- Generate inorder traversal of bst.
- Find 2 numbers whose sum is equal to k.

```cpp
class Solution {
public:
    void generate(TreeNode* root, vector<int>& inorder) {
        if(root == NULL) {
            return;
        }
		
        generate(root->left, inorder);
        inorder.push_back(root->val);
        generate(root->right, inorder);
    }
	
    bool findTarget(TreeNode* root, int k) {
        vector<int> inorder;
		
        generate(root, inorder);
		
        int left = 0;
        int right = inorder.size() - 1;
		
        while(left < right) {
            long sum = inorder[left] + inorder[right];
			
            if(sum == k) {
                return true;
            } else if(sum < k) {
                left++;
            } else {
                right--;
            }
        }
		
        return false;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |       $O(2N)$        |


### Optimal

- Create two iterator next and before. (Just like 2 pointer in array).
- next will return elements in ascending order.
- before will return elements in descending order.
- Find 2 number with sum k if exists.

```cpp

class BSTIterator {
    stack<TreeNode*> st;
    bool reverse;

public:
    BSTIterator(TreeNode* root, bool isReverse) {
        reverse = isReverse;
        pushAll(root);
    }
	
    int next() {
        TreeNode* node = st.top();
        st.pop();
		
        if(reverse) {
            pushAll(node->left);
        } else {
            pushAll(node->right);
        }
		
        return node->val;
    }
	
    bool hasNext() {
        return !st.empty();
    }
	
    void pushAll(TreeNode* root) {
        TreeNode* curr = root;
		
        while(curr) {
            st.push(curr);
			
            if(reverse) {
                curr = curr->right;
            } else {
                curr = curr->left;
            }
        }
    }
};

class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        if(!root) return false;
		
        BSTIterator l(root, false);
        BSTIterator r(root, true);
		
        int i = l.next();
        int j = r.next();
		
        while(i < j) {
            if(i + j == k) {
                return true;
            } else if(i + j < k) {
                i = l.next();
            } else {
                j = r.next();
            }
        }
		
        return false;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |       $O(2H)$        |





# References