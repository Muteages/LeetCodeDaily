# Assign Cookies

Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child i has a greed factor g[i], which is the minimum size of a cookie that the child will be content with; and each cookie j has a size s[j]. If s[j] >= g[i], we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

## Approach 

``` C++
    int findContentChildren(vector<int>& g, vector<int>& s) {
        int ans = 0;
        std::sort(g.begin(), g.end(), std::greater<int>());
        std::sort(s.begin(), s.end(), std::greater<int>());
        int child = 0;
        int cookie = 0;
        while (child < g.size())
        {
            if (cookie >= s.size())
            { // No more cookies left
                break;
            }
            if (g[child] <= s[cookie])
            { // Content the child
                ans++;
                cookie++;
            }
            child++;
        }
        return ans;
    }
```