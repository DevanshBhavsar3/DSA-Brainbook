03-02-2026  14:32

Status: #Revision

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Design Twitter

https://leetcode.com/problems/design-twitter/

- Create a min heap to efficiently remove least recent posts.
- Add posts of all the followers in the min heap.
- If min heap size is > 10, remove the least recent posts (root).
- Create ans array from the min heap and reverse it.

```cpp
class Twitter {
public:
    unordered_map<int, unordered_set<int>> following;
    unordered_map<int, vector<pair<int, int>>> posts;
    int time;
	
    Twitter() {
        time = 0;
    }
	
	// O(1)
    void postTweet(int userId, int tweetId) {
        posts[userId].push_back({time, tweetId});
        time++;
    }
	
	// O(N), N = Total posts of all the followers and self
    vector<int> getNewsFeed(int userId) {
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        vector<int> feed;
		
        for(auto post: posts[userId]) {
            pq.push(post);
			
            if(pq.size() > 10) {
                pq.pop();
            }
        }
		
        for(auto follower: following[userId]) {
            for(auto post: posts[follower]) {
                pq.push(post);
				
                if(pq.size() > 10) {
                    pq.pop();
                }
            }
        }
		
        while(!pq.empty()) {
            feed.push_back(pq.top().second);
            pq.pop();
        }
		
        reverse(feed.begin(), feed.end());
		
        return feed;
    }
    
	// O(1)
    void follow(int followerId, int followeeId) {
        following[followerId].insert(followeeId);
    }
    
	// O(1)
    void unfollow(int followerId, int followeeId) {
        following[followerId].erase(followeeId);
    }
};
```

| **Space Complexity** |
| :------------------: |
|   $O(N + U^2 + K)$   |
N = Total tweets
U = No. of users
K = Feed size (10)





# References