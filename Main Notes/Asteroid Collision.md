08-08-2025  13:41

Status: #Revision-02 n

Tags: [[Tags/DSA]] [[Stack]]

# Asteroid Collision

https://leetcode.com/problems/asteroid-collision/

- Add positive elements to the list.
- If the element is negative, remove all the smaller positive elements from the list.
- After the removal, if the top element is equal to current element, remove it.
- Else add it to the list if the stack is empty or top element is negative.

```cpp
class Solution {
public:
    vector<int> asteroidCollision(vector<int>& asteroids) {
        vector<int> st;
		
        for(int i = 0; i < asteroids.size(); i++) {
			// > 0, add to stack
            if(asteroids[i] > 0) {
                st.push_back(asteroids[i]);
            } else {
				// Remove all smaller opposite sign elements
                while(!st.empty() &&
                st.back() > 0 &&
                st.back() < abs(asteroids[i])) {
                    st.pop_back();
                }

				// If same size, remove top
                if(!st.empty() && st.back() == abs(asteroids[i])) {
                    st.pop_back();
				// If empty or negative element on top, then add negative element
                } else if(st.empty() || st.back() < 0) {
                    st.push_back(asteroids[i]);
                }
            }
        }
		
        return st;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N) + O(N)$    |        $O(N)$        |





# References