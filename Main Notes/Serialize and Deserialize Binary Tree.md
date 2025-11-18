31-10-2025  16:08

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Binary Trees]]

# Serialize and Deserialize Binary Tree

https://leetcode.com/problems/serialize-and-deserialize-binary-tree/

- Perform preorder traversal while creating a sting of the traversal.
- While deserializing create a string stream and do preorder on that.
	- If the string is #, return NULL.


```cpp
class Codec {
public:
    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if(root == NULL) {
            return "#";
        }
		
        string result = to_string(root->val) + ',';
        result += serialize(root->left);
		
        result += ',';
		
        result += serialize(root->right);
		
        return result;
    }
	
    TreeNode* helper(stringstream& stream) {
        string node;
        getline(stream, node, ',');
		
        if(node == "#") {
            return NULL;
        }
		
        TreeNode* root = new TreeNode(stoi(node));
		
        root->left = helper(stream);
        root->right = helper(stream);
		
        return root;
    }
	
    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        stringstream st(data);
        
        return helper(st);
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N) + O(N)$    |    $O(N) + O(N)$     |





# References