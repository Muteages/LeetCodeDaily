# Insert Interval

https://leetcode.com/problems/insert-interval/

You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.

Note that you don't need to modify intervals in-place. You can make a new array and return it.

## Approach 

``` C++
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        if (intervals.empty())
        {
            return {newInterval};
        }
        std::vector<std::vector<int>> ans{};
        int n = intervals.size();
        int newStart = newInterval[0], newEnd = newInterval[1];

        int idx = 0;
        // Insert all intervals which are smaller than the new Interval
        while (idx < n && intervals[idx][1] < newStart)
        {
            ans.emplace_back(intervals[idx++]);
        }
        // Cover the potential overlapping interval
        while (idx < n && intervals[idx][0] <= newEnd)
        {
            newStart = std::min(newStart, intervals[idx][0]);
            newEnd = std::max(newEnd, intervals[idx++][1]);
        }
        ans.push_back({newStart, newEnd});
        // Insert all remaining intervals
        while (idx < n)
        {
            ans.emplace_back(intervals[idx++]);
        }
        return ans;
    }
```