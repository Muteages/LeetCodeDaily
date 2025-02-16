# Construct the Lexicographically Largest Valid Sequence

https://leetcode.com/problems/construct-the-lexicographically-largest-valid-sequence

Given an integer n, find a sequence that satisfies all of the following:

The integer 1 occurs once in the sequence.
Each integer between 2 and n occurs twice in the sequence.
For every integer i between 2 and n, the distance between the two occurrences of i is exactly i.
The distance between two numbers on the sequence, a[i] and a[j], is the absolute difference of their indices, |j - i|.

Return the lexicographically largest sequence. It is guaranteed that under the given constraints, there is always a solution.


## Approach 

``` C++
class Solution {
public:

    bool isValid(int pos)
    {
        if (pos == N) return true;
        if (ans[pos] != -1) return isValid(pos + 1);

        for (int num = n - 1; num > 0; num--)
        { // Fill the possible largest number 
            if (visited[num]) continue;

            int pair = num == 1 ? pos : pos + num;
            if (pair >= N || ans[pair] != -1) continue;

            ans[pos] = ans[pair] = num;
            visited[num] = 1;

            if (isValid(pos + 1)) return true;

            ans[pos] = ans[pair] = -1;
            visited[num] = 0;
        }
        return false;
    }

    vector<int> constructDistancedSequence(int n) {
        if (n == 1) return {1};
        this->n = n;
        N = 2 * n - 1;
        ans.resize(N, -1);
        ans[0] = ans[n] = n;
        visited[n] = 1;
        isValid(1);
        return ans;
    }

private:
    std::vector<int> ans;
    std::bitset<21> visited;
    int n;
    int N;
};
```


``` Python
    def constructDistancedSequence(self, n: int) -> List[int]:
        if n == 1:
            return [1]

        N = 2 * n - 1
        ans = [-1] * N
        ans[0] = ans[n] = n
        visited = [0] * (n + 1)
        visited[n] = 1

        def is_valid(pos: int) -> bool:
            if pos == N:
                return True
            
            if ans[pos] != -1:
                return is_valid(pos + 1)
            
            for num in range(n - 1, 0, -1):
                if visited[num]:
                    continue
                
                pair = pos if num == 1 else pos + num
                if pair >= N or ans[pair] != -1:
                    continue
                
                ans[pos] = ans[pair] = num
                visited[num] = 1

                if is_valid(pos + 1):
                    return True
                
                # backtracking reset
                ans[pos] = ans[pair] = -1
                visited[num] = 0
            
            return False
        
        is_valid(1)
        return ans
```

