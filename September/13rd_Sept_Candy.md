# Candy

https://leetcode.com/problems/candy/description

There are n children standing in a line. Each child is assigned a rating value given in the integer array ratings.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy.
Children with a higher rating get more candies than their neighbors.
Return the minimum number of candies you need to have to distribute the candies to the children.


## Approach 1

``` C++
    int candy(vector<int>& ratings) {
      int n = ratings.size();
      std::vector<int> candies(n, 1);

      for (int i = 1; i < n; i++)
      { // Check left neighbour
        if (ratings[i] > ratings[i - 1])
        {
          candies[i] = candies[i - 1] + 1;
        }
      }

      for (int i = n - 2; i >= 0; i--)
      { // Check right neighbour
        if (ratings[i] > ratings[i + 1])
        {
          candies[i] = std::max(candies[i], candies[i + 1] + 1);
        }
      }

      int ans = std::accumulate(candies.begin(), candies.end(), 0);
      return ans;  
    }
```


## Approach 2 

``` C++
    int candy(vector<int>& ratings) {
        int up = 0, down = 0, peak = 0;
        int cnt = 1;

        for (int i = 1; i < ratings.size(); i++)
        {
          if (ratings[i] > ratings[i - 1])
          { // Increase case
            up++;
            peak = up + 1;
            down = 0;
            cnt += peak;
          }

          else if (ratings[i] == ratings[i - 1])
          { // Equal case
            up = 0;
            down = 0;
            peak = 0;
            cnt++;
          }

          else
          { // Decrease case
            up = 0;
            down++;
            cnt += down + 1 - (peak > down);
          }
        }

        return cnt;
    }
```