15-08-2025  15:16

Status: #Revision-03

Tags: [[Tags/DSA]] [[Stack]]

# The Celebrity Problem

https://www.geeksforgeeks.org/problems/the-celebrity-problem/1

## Brute Force

- Create an array to count how many people I know.
- And how many people know me.
- For every element in the matrix, if the element is 1. increase i's I know count and j's know me count.
- At the end, return the person with 1 I know count and N know me count.

```cpp
class Solution {
  public:
    int celebrity(vector<vector<int> >& mat) {
        vector<int> knowMe (mat.size(), 0);
        vector<int> iknow (mat.size(), 0);
        
        for(int i = 0; i < mat.size(); i++) {
            for(int j = 0; j < mat[0].size(); j++) {
                if(mat[i][j] == 1) {
                    knowMe[j]++;
                    iknow[i]++;
                }
            }
        }
        
        for(int i = 0; i < knowMe.size(); i++) {
            if((knowMe[i] == mat.size()) && iknow[i] == 1) {
                return i;
            }
        }
        
        return -1;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(N * N) + O(N)$  |       $O(2N)$        |


## Optimal

- Create 2 pointers top and down.
- If top knows down, top can't be the celebrity, so increase top.
- Else if bottom knows top, bottom can't be celebrity, so decrease bottom.
- If any of them don't know each other, both can't be the celebrity.
- At the end, check if everyone know top and top knows no one.

```cpp
class Solution {
  public:
    int celebrity(vector<vector<int> >& mat) {
        int top = 0;
        int bottom = mat.size() - 1;
        
        while(top < bottom) {
            if(mat[bottom][top] == 1) {
                bottom--;
            } else if(mat[top][bottom] == 1) {
                top++;
            } else {
                top++;
                bottom--;
            }
        }
        
        if(top != bottom) {
            return -1;
        }
        
        
        for(int i = 0; i < mat.size(); i++) {
            if(i == top) continue;
            
            if(mat[top][i] == 1 || mat[i][top] == 0) {
                return -1;
            }
        }
        
        return top;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(1)$        |





# References