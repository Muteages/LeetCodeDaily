# Design a Stack with Increment Operation

https://leetcode.com/problems/design-a-stack-with-increment-operation

Design a stack that supports increment operations on its elements.

Implement the CustomStack class:

CustomStack(int maxSize) Initializes the object with maxSize which is the maximum number of elements in the stack.
void push(int x) Adds x to the top of the stack if the stack has not reached the maxSize.
int pop() Pops and returns the top of the stack or -1 if the stack is empty.
void inc(int k, int val) Increments the bottom k elements of the stack by val. If there are less than k elements in the stack, increment all the elements in the stack.

## Approach 

``` C++
class CustomStack {
public:
    CustomStack(int maxSize) :
        maxSize(maxSize) 
    {
        st.reserve(maxSize);    
    }
    
    void push(int x) {
        if (st.size() == maxSize) return;
        st.emplace_back(x);
    }
    
    int pop() {
        if (st.empty()) return -1;
        int p = st.back();
        st.pop_back();
        return p;
    }
    
    void increment(int k, int val) {
        int n = st.size();
        for (int i = 0; i < std::min(k, n); i++)
        {
            st[i] += val;
        }
    }
private:
    std::vector<int> st;
    int maxSize;
};
```