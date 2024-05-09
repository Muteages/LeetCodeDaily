# Maximise Happiness of Selected Children

https://leetcode.com/problems/maximize-happiness-of-selected-children

You are given an array happiness of length n, and a positive integer k.

There are n children standing in a queue, where the ith child has happiness value happiness[i]. You want to select k children from these n children in k turns.

In each turn, when you select a child, the happiness value of all the children that have not been selected till now decreases by 1. Note that the happiness value cannot become negative and gets decremented only if it is positive.

Return the maximum sum of the happiness values of the selected children you can achieve by selecting k children.

## Approach 

``` C++
    long long maximumHappinessSum(vector<int>& happiness, int k) {
        std::sort(happiness.rbegin(), happiness.rend());       
        long long ans = 0;
        for(int i = 0; i < k; i++) 
        {
            int h = happiness[i] - i;
            if (h <= 0)
            {
                break;
            }
            ans += h;
        }
        return ans;
    }
```

