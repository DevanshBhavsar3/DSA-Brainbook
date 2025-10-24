26-09-2025  14:42

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Candy

https://leetcode.com/problems/candy/

### Brute Force

- First check for the left neighbors, if the ratings is > assign 1 more than its left.
- Then check for the right neighbors, if the ratings is > assign 1 more than its right.
- Get sum of the max(left, right).

```cpp
class Solution {
public:
    int candy(vector<int>& ratings) {
        vector<int> left(ratings.size(), 1);
        vector<int> right(ratings.size(), 1);
        int total = 0;
        
        for(int i = 1; i < ratings.size(); i++) {
            if(ratings[i] > ratings[i - 1]) {
                left[i] = left[i - 1] + 1;
            }
        }
        
        for(int i = ratings.size() - 2; i >= 0; i--) {
            if(ratings[i] > ratings[i + 1]) {
                right[i] = right[i + 1] + 1;
            }
        }
        
        for(int i = 0; i < ratings.size(); i++) {
            total += max(left[i], right[i]);
        }
        
        return total;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(3N)$       |       $O(2N)$        |


### Better

- First check for the left neighbors, if the ratings is > assign 1 more than its left.
- Instead of checking for right neighbors and then finding sum, calculate sum on the fly.

```cpp
class Solution {
public:
    int candy(vector<int>& ratings) {
        vector<int> left(ratings.size(), 1);
        
        for(int i = 1; i < ratings.size(); i++) {
            if(ratings[i] > ratings[i - 1]) {
                left[i] = left[i - 1] + 1;
            }
        }
        
        // IMPORTANT: Last element will be ignored while counting sum
        int total = max(1, left[ratings.size() - 1]);
        
        int right = 1; // Right neighbor
        int curr = 1; // Curr candies
        
        for(int i = ratings.size() - 2; i >= 0; i--) {
            if(ratings[i] > ratings[i + 1]) {
                curr = right + 1;
            } else {
                curr = 1;
            }
            
            right = curr;
            total += max(left[i], curr);
        }
        
        return total;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(2N)$       |        $O(N)$        |


### Optimal

![[Pasted image 20250926152936.png]]

- Imagine the ratings as slop.
- When you get flat slop, just increase total by 1.
- Else go till the peak of the slop, while adding the candies.
- Then go till the ground, while adding the candies.
- Change the peak, and update the total if needed.

```cpp
class Solution {
public:
    int candy(vector<int>& ratings) {
        int total = 1;
        
        int i = 1;
        
        while(i < ratings.size()) {
            if(ratings[i] == ratings[i - 1]) {
                total += 1;
                i++;
                continue;
            }
            
            int peak = 1;
            
            while(i < ratings.size() && ratings[i] > ratings[i - 1]) {
                peak++;
                total += peak;
                i++;
            }
            
            int down = 1;
            
            while(i < ratings.size() && ratings[i] < ratings[i - 1]) {
                total += down;
                down++;
                i++;
            }
            
            if(down > peak) {
                total += down - peak;
            }
        }
        
        return total;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References