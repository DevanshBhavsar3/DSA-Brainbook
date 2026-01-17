12-01-2026  16:08

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Accounts Merge

https://leetcode.com/problems/accounts-merge/

- Treat index of every account as a node in disjoint set.
- Map each email to their index. If the email is already mapped to some index, perform union between the 2 indices.
- Map all the emails to their ultimate parent from the DSU.
- Create the ans array from the merged mails.

```cpp
class DisjointSet {
public:
    vector<int> parent, size;
	
    DisjointSet(int n) {
        size.resize(n, 1);
        parent.reserve(n);
		
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
	
    int findParent(int node) {
        if (parent[node] == node) {
            return node;
        }
		
        return parent[node] = findParent(parent[node]);
    }
	
    void unionBySize(int u, int v) {
        int pU = findParent(u);
        int pV = findParent(v);
		
        if (pU == pV) {
            return;
        }
		
        if (size[pU] < size[pV]) {
            parent[pU] = pV;
            size[pV] += size[pU];
        } else {
            parent[pV] = pU;
            size[pU] += size[pV];
        }
    }
};

class Solution {
public:
    vector<vector<string>> accountsMerge(vector<vector<string>>& accounts) {
        vector<vector<string>> mergedMails(accounts.size());
        vector<vector<string>> mergedAccounts;
        DisjointSet ds(accounts.size());
        map<string, int> mp;
		
		// O(M * 4 alpha)
        for (int i = 0; i < accounts.size(); i++) {
            for (int j = 1; j < accounts[i].size(); j++) {
                string mail = accounts[i][j];
				
                if (mp.find(mail) != mp.end()) {
                    ds.unionBySize(i, mp[mail]);
                } else {
                    mp[mail] = i;
                }
            }
        }
		
		// O(M)
        for (auto& it : mp) {
            string mail = it.first;
            int parent = ds.findParent(it.second);
			
            mergedMails[parent].push_back(mail);
        }
		
		// O(N + M)
        for (int i = 0; i < mergedMails.size(); i++) {
            if (mergedMails[i].size() == 0) {
                continue;
            }
			
            vector<string> account;
			
            account.push_back(accounts[i][0]);
			
            for (auto& it : mergedMails[i]) {
                account.push_back(it);
            }
			
            mergedAccounts.push_back(account);
        }
		
        return mergedAccounts;
    }
};
```

|     **Time Complexity**      | **Space Complexity** |
| :--------------------------: | :------------------: |
| $O(M * 4\alpha + M + N + M)$ |     $O(4N + 3M)$     |
N = No. of account
M = No. of mails





# References