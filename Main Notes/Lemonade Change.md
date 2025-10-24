22-09-2025  14:35

Status: #Revision-02  

Tags: [[Tags/DSA|DSA]] [[Greedy Algorithms]]

# Lemonade Change

https://leetcode.com/problems/lemonade-change/

- Create variables for fives and tens.
- If bill is of 5, then add it to fives.
- Else if bill is of 10, give change of 5 if you have.
- Else bill is of 20, then first give fives and tens, if you don't have tens give 3 fives.

```cpp
class Solution {
public:
    bool lemonadeChange(vector<int>& bills) {
        int fives = 0;
        int tens = 0;
        
        for(int i = 0; i < bills.size(); i++) {
            if(bills[i] == 5) {
                fives++;
            } else if(bills[i] == 10) {
                if(fives == 0) {
                    return false;
                }
                
                fives--;
                tens++;
            } else {
                if(fives && tens) {
                    fives--;
                    tens--;
                } else if(fives >= 3) {
                    fives -= 3;
                } else {
                    return false;
                }
            }
        }
        
        return true;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(1)$        |





# References