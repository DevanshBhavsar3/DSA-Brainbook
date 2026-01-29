16-08-2025  16:49

Status: #Revision-03

Tags: [[Tags/DSA]] [[Stack]]

# LFU Cache

https://leetcode.com/problems/lfu-cache/

- For each frequency create a new LRU cache.
- For get function,
	- Check if the key is in the map, return if -1 if not.
	- Move the node to the next frequency's list.
- For put function,
	- If key is in the map, update the node's value and move it to the next frequency's list.
	- If the capacity is reached, delete last node from the minFreq list.
	- Update minFreq to 1, create new node and add it to the frequency list of 1 and in the key map.


```cpp
struct Node {
    int key;
    int value;
    int frequency;
    Node* prev;
    Node* next;
	
    Node(int key, int value, int frequency, Node* prev, Node* next) {
        this->key = key;
        this->value = value;
        this->frequency = frequency;
        this->prev = prev;
        this->next = next;
    }
};

class DoubleyLinkedList {
public:
    Node* head;
    Node* tail;
    int length;
	
    DoubleyLinkedList() {
        tail = new Node(-1, -1, 0, NULL, NULL);
        head = new Node(-1, -1, 0, NULL, tail);
        
        tail->prev = head;
        
        length = 0;
    }
	
    void insertAfterHead(Node* node) {
        node->next = head->next;
        node->prev = head;
		
        head->next->prev = node;
        head->next = node;
		
        length++;
    }
	
    void deleteNode(Node* node) {
        node->next->prev = node->prev;
        node->prev->next = node->next;
		
        node->prev = NULL;
        node->next = NULL;
		
        length--;
    }
};

class LFUCache {
public:
    map<int, DoubleyLinkedList*> freqList;
    map<int, Node*> keyNode;
    int minFreq;
    int capacity;
	
    LFUCache(int capacity) {
        freqList[1] = new DoubleyLinkedList();
        minFreq = 1;
        this->capacity = capacity;
    }
	
	// O(1)
    int get(int key) {
        if(keyNode.find(key) == keyNode.end()) {
            return -1;    
        }
		
        Node* node = keyNode[key];
        updateFrequency(node);
       
        return node->value;
    }
	
	// O(1)
    void put(int key, int value) {
        if(keyNode.find(key) != keyNode.end()) {
            Node* node = keyNode[key];
            node->value = value;
			
            updateFrequency(node);
            return;
        }
		
        if(keyNode.size() == capacity) {
            Node* lru = freqList[minFreq]->tail->prev;
			
            keyNode.erase(lru->key); // IMPORTANT
            freqList[minFreq]->deleteNode(lru);
            delete lru;
        }
		
        minFreq = 1;
		
        Node* node = new Node(key, value, 1, NULL, NULL);
        
        freqList[minFreq]->insertAfterHead(node);
        keyNode[key] = node;
    }
	
    void updateFrequency(Node* node) {
        int currFrequency = node->frequency;
		
		// Create a new list if not exists in the next frequency
        if(freqList.find(currFrequency + 1) == freqList.end()) {
            freqList[currFrequency + 1] = new DoubleyLinkedList(); 
        }
		
		// Delete node from current list
        freqList[currFrequency]->deleteNode(node);
		
		// Add node to next frequency list
        freqList[currFrequency + 1]->insertAfterHead(node);
		
		// Update min frequency if the current frequency's list is empty
        if(minFreq == currFrequency && freqList[minFreq]->length == 0) {
            minFreq++;
        }
		
		// Update the node's frequency
        node->frequency++;
    }
};
```

|                              **Time Complexity**                               |
| :----------------------------------------------------------------------------: |
| $O(\log n)$ (Map), <br><br>$O(n)$ (Unordered Map)<br>$O(n^2)$ (Worst Case)<br> |
For N function calls,




# References

[[LRU Cache]]