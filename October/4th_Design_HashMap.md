# Design HashMap

https://leetcode.com/problems/design-hashmap

Design a HashMap without using any built-in hash table libraries.


## Approach

``` C++
class MyHashMap {
public:
    MyHashMap() 
        : size(10000)
    {
        ump.resize(size);
    }
    
    void put(int key, int value) {
        int index = key % size; // hash seed
        auto& curr = ump[index];
        for (auto& [k, v] : curr)
        { // Check if it exists
            if (k == key)
            {
                v = value;
                return;
            }
        }
        // Or add a new one
        curr.emplace_back(key, value);

    }
    
    int get(int key) {
        int index = key % size;
        auto& curr = ump[index];
        for (auto& [k, v] : curr)
        {
            if (k == key)
            {
                return v;
            }
        }
        return -1;
    }
    
    void remove(int key) {
        int index = key % size;
        auto& curr = ump[index];
        for (auto it = curr.begin(); it != curr.end(); it++)
        {
            if (it->first == key)
            {
                curr.erase(it);
                return;
            }
        }
    }

private:
    std::vector<std::list<std::pair<int, int>>> ump;
    const int size;
};
```