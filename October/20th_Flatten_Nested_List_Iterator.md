# Flatten Nested List Iterator

https://leetcode.com/problems/flatten-nested-list-iterator

You are given a nested list of integers nestedList. Each element is either an integer or a list whose elements may also be integers or other lists. Implement an iterator to flatten it.

Implement the NestedIterator class:

NestedIterator(List<NestedInteger> nestedList) Initializes the iterator with the nested list nestedList.
int next() Returns the next integer in the nested list.
boolean hasNext() Returns true if there are still some integers in the nested list and false otherwise.
Your code will be tested with the following pseudocode:

initialize iterator with nestedList
res = []
while iterator.hasNext()
    append iterator.next() to the end of res
return res
If res matches the expected flattened list, then your code will be judged as correct.


## Approach 1

Recursion
``` C++
class NestedIterator {
public:
    NestedIterator(vector<NestedInteger> &nestedList) 
        : index(0)
    {
        flatten.clear();
        processList(nestedList);
    }
    
    int next() {
        return flatten[index++];
    }
    
    bool hasNext() {
        return index < flatten.size();
    }
private:
    void processList(vector<NestedInteger> &list)
    {
        for (auto& ele : list)
        {
            if (ele.isInteger())
            {
                flatten.emplace_back(ele.getInteger());
            }
            else
            {
                processList(ele.getList());
            }
        }
    }

private:
    int index;
    std::vector<int> flatten;
};
```

## Approach 2

``` C++
class NestedIterator {
    std::stack<NestedInteger> st;
public:
    NestedIterator(vector<NestedInteger> &nestedList) {
        for (int i = nestedList.size() - 1; i >= 0; i--)
        {
            st.push(nestedList[i]);
        }
    }
    
    int next() {
        int num = st.top().getInteger();
        st.pop();
        return num;
    }
    
    bool hasNext() {
        while (!st.empty())
        {
            auto curr = st.top();
            if (curr.isInteger())
            { // Single integer, jump to next() func to read the number
                return true;
            }
            else
            {
                st.pop();
                auto list = curr.getList();
                for (int i = list.size() - 1; i >= 0; i--)
                {
                    st.push(list[i]);
                }
            }
        }
        return false;
    }
};
```