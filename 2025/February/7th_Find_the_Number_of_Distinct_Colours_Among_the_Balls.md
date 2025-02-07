# Find the Number of Distinct Colors Among the Balls

https://leetcode.com/problems/find-the-number-of-distinct-colors-among-the-balls

You are given an integer limit and a 2D array queries of size n x 2.

There are limit + 1 balls with distinct labels in the range [0, limit]. Initially, all balls are uncolored. For every query in queries that is of the form [x, y], you mark ball x with the color y. After each query, you need to find the number of distinct colors among the balls.

Return an array result of length n, where result[i] denotes the number of distinct colors after ith query.

Note that when answering a query, lack of a color will not be considered as a color.


## Approach 

``` C++
    vector<int> queryResults(int limit, vector<vector<int>>& queries) {
        const int n = queries.size();
        std::unordered_map<int, int> colourFreq;
        std::unordered_map<int, int> ballColour;
        std::vector<int> ans{};
        ans.reserve(n);
        int curColourCnt = 0;
        for (const auto& q : queries)
        {
            int ball = q[0], colour = q[1];
            if (ballColour[ball] > 0)
            { // Recolour the ball
                int prevColour = ballColour[ball];
                if (--colourFreq[prevColour] == 0)
                {
                    curColourCnt--;
                }
                
            }
            ballColour[ball] = colour;
            if (++colourFreq[colour] == 1)
            { // Added a new colour
                curColourCnt++;
            }

            ans.emplace_back(curColourCnt);
        }
        return ans;
    }
```

``` Python
    def queryResults(self, limit: int, queries: List[List[int]]) -> List[int]:
        ball_colour = defaultdict(int)
        colour_freq = defaultdict(int)
        ans = []
        colour_cnt = 0
        for b, c in queries:
            if b in ball_colour:
                prev_colour = ball_colour[b]
                colour_freq[prev_colour] -= 1
                if colour_freq[prev_colour] == 0:
                    colour_cnt -= 1
            
            ball_colour[b] = c
            colour_freq[c] += 1
            if colour_freq[c] == 1:
                colour_cnt += 1
            ans.append(colour_cnt)
        return ans
```

``` JavaScript
var queryResults = function(limit, queries) {
    const bc = new Map(), cf = new Map(), ans = [];
    let cnt = 0;
    for (const [b, c] of queries) {
        if (bc.has(b)) {
            let prevC = bc.get(b);
            cf.set(prevC, cf.get(prevC) - 1);
            if (cf.get(prevC) === 0) {
                cnt--;
            }
        }
        bc.set(b, c);
        cf.set(c, (cf.get(c) || 0) + 1);
        if (cf.get(c) === 1) {
            cnt++;
        }
        ans.push(cnt);
    }
    return ans;
};
```