24-12-2025  17:16

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Alien Dictionary

https://www.naukri.com/code360/problems/alien-dictionary_630423

- Find the point of difference between pair of words in the dictionary.
- Create a directed graph based on the differences.
- Perform topological sort on the graph.

```cpp
string getAlienLanguage(vector<string> &dictionary, int k)
{
    vector<vector<int>> adj(k);
    vector<int> indegree(k);
    string lang;
    queue<int> q;
	
    for(int i = 1; i < dictionary.size(); i++) {
        string u = dictionary[i - 1];
        string v = dictionary[i];
		
        int idx = 0;
        int len = min(u.size(), v.size());
		
		// Finding the point of difference
        for(int i = 0; i < len; i++) {
            if(u[i] != v[i]) {
				// Create an edge
                adj[u[i] - 'a'].push_back(v[i] - 'a');
                indegree[v[i] - 'a']++;
                break;
            }
        }
    }
	
    for(int i = 0; i < indegree.size(); i++) {
        if(indegree[i] == 0) {
            q.push(i);
        }
    }
	
    while(!q.empty()) {
        int node = q.front();
        q.pop();
		
        lang.push_back('a' + node);
		
        for(auto it: adj[node]) {
            indegree[it]--;
			
            if(indegree[it] == 0) {
                q.push(it);
            }
        }
    }
	
    return lang;
}
```

|  **Time Complexity**  | **Space Complexity** |
| :-------------------: | :------------------: |
| $O((N * K) + 2K + E)$ |     $O(4K + E)$      |


### Testcases when the solution fails

1. When the larger word appear before shorter word in the dictionary and all the chars are same.
Example,
```
abcd
abc
```

2. When there is cyclic dependency.
Example,
```
abc
bac
acb
```





# References