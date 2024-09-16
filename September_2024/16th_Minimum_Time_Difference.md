# Minimum Time Difference

https://leetcode.com/problems/minimum-time-difference

Given a list of 24-hour clock time points in "HH:MM" format, return the minimum minutes difference between any two time-points in the list.

## Approach 1

``` C++
    int findMinDifference(vector<string>& timePoints) {
        int n = timePoints.size();
        std::vector<int> mins(n);
        for (int i = 0; i < n; i++)
        {
            int hour = std::stoi(timePoints[i].substr(0, 2));
            int minute = std::stoi(timePoints[i].substr(3, 2));
            mins[i] = 60 * hour + minute;
        }
        std::sort(mins.begin(), mins.end());

        int ans = 720; // 60 * 12;
        for (int i = 1; i < n; i++)
        {
            ans = std::min(ans, mins[i] - mins[i - 1]);
            if (ans == 0) return ans;
        }

        // Handle the first and last time points
        ans = std::min(ans, 1440 - (mins.back() - mins.front()));
        return ans;
    }
```

## Approach 2

``` C++
    int findMinDifference(vector<string>& timePoints) {
        int MAX = 60 * 24;
        int minMin = MAX, maxMin = -1;
        std::vector<bool> visited(MAX, false);
        for (const auto& time : timePoints)
        {
            int mins = ((time[0] - '0') * 10 + (time[1] - '0')) * 60 + ((time[3] - '0') * 10 + (time[4] - '0'));
            if (visited[mins]) return 0; // Have two same points
            visited[mins] = 1;
            minMin = std::min(minMin, mins);
            maxMin = std::max(maxMin, mins);
        }

        int ans = MAX - (maxMin - minMin); // Handle the first and last points.
        int prev = minMin;
        for (int curr = minMin + 1; curr <= maxMin; curr++)
        {
            if (!visited[curr]) continue;
            ans = std::min(ans, curr - prev);
            prev = curr;
        }
        return ans;
    }
```

``` JavaScript
var findMinDifference = function(timePoints) {
    const MAX = 60 * 24;
    let max = -1, min = MAX;
    const visited = Array(MAX).fill(0);
    for (let time of timePoints) {
        let [h, m] = time.split(':');
        let mins = Number(h) * 60 + Number(m); // ~~h || +h || h * 1
        if (visited[mins]) return 0;

        visited[mins] = 1;
        max = Math.max(max, mins);
        min = Math.min(min, mins);
    }

    let ans = MAX - (max - min);
    let prev = min;
    for (let curr = min + 1; curr <= max; curr++) {
        if (!visited[curr]) continue;

        ans = Math.min(ans, curr - prev);
        prev = curr;
    }
    return ans;
};
```