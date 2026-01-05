02-01-2026  15:04

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Graphs]]

# Minimum Multiplications to reach End

https://www.geeksforgeeks.org/problems/minimum-multiplications-to-reach-end/1

- Perform a simple BFS with a visited array. 
- The source node is the start, multiply the node with all the elements of an array.
- Add the new value to the queue if it is not visited.

```cpp
class Solution {
  public:
    int minimumMultiplications(vector<int>& arr, int start, int end) {
        queue<pair<int, int>> q;
        vector<int> visited(100000, 0);
        
        q.push({start, 0});
        visited[start] = 1;
        
        while(!q.empty()) {
            auto [value, steps] = q.front();
            q.pop();
            
            if(value == end) {
                return steps;
            }
            
            for(int& it: arr) {
                int newValue = ((long) value * it) % 100000;
                
                if(!visited[newValue]) {
                    q.push({newValue, steps + 1});
                    visited[newValue] = 1;
                }
            }
        }
        
        return -1;
    }
};
```

|  **Time Complexity**  | **Space Complexity** |
| :-------------------: | :------------------: |
| $O(\approx 10^5 * N)$ |      $O(10^5)$       |





# References