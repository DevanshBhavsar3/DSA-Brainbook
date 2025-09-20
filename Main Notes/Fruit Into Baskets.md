15-09-2025  18:43

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Sliding Window & Two Pointers Problems]]

# Fruit Into Baskets

https://leetcode.com/problems/fruit-into-baskets/description/

### Brute Force

- Find the subarray with maximum no. of fruits of 2 types.

```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        int maxFruits = 0;
        
        for(int i = 0; i < fruits.size(); i++) {
            int basket1 = -1;
            int basket2 = -1;
            
            int total = 0;
            
            for(int j = i; j < fruits.size(); j++) {
                if(basket1 == -1 && fruits[j] != basket2) {
                    basket1 = fruits[j];
                    total++;
                } else if(basket2 == -1 && fruits[j] != basket1) {
                    basket2 = fruits[j];
                    total++;
                } else if(fruits[j] == basket1 || fruits[j] == basket2) {
                    total++;
                } else {
                    break;
                }
            }
            
            maxFruits = max(maxFruits, total);
        }
        
        return maxFruits;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|      $O(N^2)$       |        $O(1)$        |


### Better

- Create a sliding window with at most 2 unique numbers.
- If the window has more than 2 unique numbers, move left until 1 numbers is removed from the window.

```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        map<int, int> mp;
        
        int left = 0;
        int right = 0;
        
        int maxFruits = 0;
        
        while(right < fruits.size()) {
            mp[fruits[right]]++;
            
            while(mp.size() > 2) {
                mp[fruits[left]]--;
                
                if(mp[fruits[left]] == 0) {
                    mp.erase(fruits[left]);
                }
                
                left++;
            }
            
            maxFruits = max(maxFruits, right - left + 1);
            
            right++;
        }
        
        return maxFruits;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(1)$        |


### Optimal

- Create a sliding window with at most 2 unique numbers.
- If unique numbers > 2, move both left and right.
- Only update the ans, if the unique numbers are <= 2.

```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        map<int, int> mp;
        
        int left = 0;
        int right = 0;
        
        int maxFruits = 0;
        
        while(right < fruits.size()) {
            mp[fruits[right]]++;
            
            if(mp.size() > 2) {
                mp[fruits[left]]--;
                
                if(mp[fruits[left]] == 0) {
                    mp.erase(fruits[left]);
                }
                
                left++;
            }
            
            if(mp.size() <= 2) {
                maxFruits = max(maxFruits, right - left + 1);
            }
            
            right++;
        }
        
        return maxFruits;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References