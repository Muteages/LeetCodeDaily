# Insert Delete GetRandom O(1)

https://leetcode.com/problems/insert-delete-getrandom-o1

Implement the RandomizedSet class:

RandomizedSet() Initializes the RandomizedSet object.
bool insert(int val) Inserts an item val into the set if not present. Returns true if the item was not present, false otherwise.
bool remove(int val) Removes an item val from the set if present. Returns true if the item was present, false otherwise.
int getRandom() Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the same probability of being returned.
You must implement the functions of the class such that each function works in average O(1) time complexity.


## Approach 
``` C++
private:
    std::vector<int> idx;
    std::unordered_map<int, int> rs; // Value - value index at idx
    //int sz;
public:
    RandomizedSet() {
        idx.clear();
    }
    
    bool insert(int val) {
        if (rs.find(val) != rs.end())
        { // The value exists.
            return false;
        }

        idx.emplace_back(val);
        rs[val] = idx.size() - 1;
        return true;
    }
    
    bool remove(int val) {
        if (rs.find(val) == rs.end())
        { // The value doesn't exist
            return false;
        }

        auto it = rs.find(val); 

        // Replace the value with the last element in idx array and update its index
        idx[it->second] = idx.back(); 
        rs[idx.back()] = it->second;

        // Delete the last element in idx and val in rs
        idx.pop_back();
        rs.erase(val);

        return true;
    }
    
    int getRandom() {
        return idx[rand() % idx.size()];
    }
```