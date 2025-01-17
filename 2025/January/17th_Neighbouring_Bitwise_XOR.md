# Neighbouring Bitwise XOR

https://leetcode.com/problems/neighboring-bitwise-xor

A 0-indexed array derived with length n is derived by computing the bitwise XOR (⊕) of adjacent values in a binary array original of length n.

Specifically, for each index i in the range [0, n - 1]:

If i = n - 1, then derived[i] = original[i] ⊕ original[0].
Otherwise, derived[i] = original[i] ⊕ original[i + 1].
Given an array derived, your task is to determine whether there exists a valid binary array original that could have formed derived.

Return true if such an array exists or false otherwise.


## Approach 

Since x1 ^ x2 = y1, x2 ^ x3 = y2 ... xn ^ x0 = yn.   y1 ^ y2 ^ ... ^ yn = 0

``` C++
    bool doesValidArrayExist(vector<int>& derived) {
        return std::accumulate(derived.begin(), derived.end(), 0, std::bit_xor<int>()) == 0;
    }
```


``` Python
    def doesValidArrayExist(self, derived: List[int]) -> bool:
        return reduce(ixor, derived) == 0
```

``` JavaScript
var doesValidArrayExist = function(derived) {
    return derived.reduce((acc, ele) => acc ^ ele) === 0;
};
```