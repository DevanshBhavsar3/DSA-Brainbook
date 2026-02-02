01-02-2026  16:10

Status: #Revision 

Tags: [[Tags/DSA|DSA]] [[Heaps]]

# Merge K Sorted Lists

https://leetcode.com/problems/merge-k-sorted-lists/

## Brute Force

- Create a single linked list from all the k linked list.
- Sort that LL and return it.

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|  $O(N + N \log N)$  |        $O(N)$        |


## Optimal

- First, create a min heap from the heads of K linked lists.
- While the min heap is not empty, add the root of the min heap to ans LL and push the next node to the min heap. 

```cpp
class Compare {
public:
    bool operator()(ListNode* a, ListNode* b) {
        return a->val > b->val;
    }    
};

class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, Compare> pq;
        ListNode* sorted = new ListNode(-1, NULL);
        ListNode* curr = sorted;
		
        for(int i = 0; i < lists.size(); i++) {
            if(lists[i]) {
                pq.push(lists[i]);
            }
        }
		
        while(!pq.empty()) {
            ListNode* node = pq.top();
            pq.pop();
			
            if(node->next) {
                pq.push(node->next);
            }
			
            curr->next = node;
            curr = curr->next;
        }
		
        return sorted->next;   
    }
};
```

| **Time Complexity** | **Space Complexity** |
| :-----------------: | :------------------: |
|    $O(N \log K)$    |        $O(K)$        |





# References