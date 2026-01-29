14-08-2025  15:52

Status: #Revision-03

Tags: [[Tags/DSA]] [[Stack]]

# Online Stock Span

https://leetcode.com/problems/online-stock-span/description/

## Brute Force

- Find total consecutive prices that are <= current price from the back. 
- Add the current price to prices list.

```cpp
class StockSpanner {
public:
    vector<int> prices;
	
    StockSpanner() {
        
    }
    
    int next(int price) {
        int span = 1;
		
        for(int i = prices.size() - 1; i >= 0; i--) {
            if(prices[i] > price) {
                break;
            }
			
            span++;
        }
		
        prices.push_back(price);
		
        return span;
    }
};
```

|     **Time Complexity**     |  **Space Complexity**  |
| :-------------------------: | :--------------------: |
| $O(x)$, x = current day no. | $O(N)$, N = total days |


## Optimal

- Create a monotonic stack for decreasing elements. ( Previous Greater Element )
- Subtract previous greater price's day from current day.

```cpp
class StockSpanner {
public:
    stack<pair<int, int>> st;
    int day;
	
    StockSpanner() {
        day = -1;
    }
    
    int next(int price) {
        day++;
		
        while(!st.empty() && price >= st.top().first) {
            st.pop();
        }
		
        int ans = day - (st.empty() ? -1 : st.top().second);
        st.push({price, day});
		
        return ans;
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|       $O(N)$        |        $O(N)$        |





# References

[[Next Greater Element I]]