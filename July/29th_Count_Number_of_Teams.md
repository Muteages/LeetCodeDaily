# Count Number of Teams

https://leetcode.com/problems/count-number-of-teams

There are n soldiers standing in a line. Each soldier is assigned a unique rating value.

You have to form a team of 3 soldiers amongst them under the following rules:

Choose 3 soldiers with index (i, j, k) with rating (rating[i], rating[j], rating[k]).
A team is valid if: (rating[i] < rating[j] < rating[k]) or (rating[i] > rating[j] > rating[k]) where (0 <= i < j < k < n).
Return the number of teams you can form given the conditions. (soldiers can be part of multiple teams).


## Approach 

``` C++
    int makeTeams(const std::vector<int>& rating, int mid)
    {
        int leftSmaller{}, leftGreater{}, rightSmaller{}, rightGreater{};
        int l = mid - 1, r = mid + 1;
        while (l >= 0)
        {
            leftSmaller += rating[l] < rating[mid];
            leftGreater += rating[l] > rating[mid];
            l--;
        }
        while (r < rating.size())
        {
            rightSmaller += rating[r] < rating[mid];
            rightGreater += rating[r] > rating[mid];
            r++;
        }
        return leftSmaller * rightGreater + leftGreater * rightSmaller;
    }

    int numTeams(vector<int>& rating) {
        int ans = 0;
        for (int i = 0; i < rating.size(); i++)
        {
            ans += makeTeams(rating, i);
        }
        return ans;
    }
```