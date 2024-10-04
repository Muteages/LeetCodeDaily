# Divide Players into Teams of Equal Skill

https://leetcode.com/problems/divide-players-into-teams-of-equal-skill

You are given a positive integer array skill of even length n where skill[i] denotes the skill of the ith player. Divide the players into n / 2 teams of size 2 such that the total skill of each team is equal.

The chemistry of a team is equal to the product of the skills of the players on that team.

Return the sum of the chemistry of all the teams, or return -1 if there is no way to divide the players into teams such that the total skill of each team is equal.

## Approach 1

Sort && Greedy
``` C++
    long long dividePlayers(vector<int>& skill) {
        const int n = skill.size();
        std::sort(skill.begin(), skill.end());
        long long ans = 0;
        int targetSum = skill[0] + skill[n - 1];
        for (int i = 0, j = n - 1; i < j; i++, j--)
        {
            if (skill[i] + skill[j] != targetSum)
            {
                return -1;
            }
            ans += static_cast<long long>(skill[i]) * skill[j];
        }
        return ans;
    }
```

## Approach 2

Counting && Greedy

``` JavaScript
var dividePlayers = function(skill) {
    const freq = new Array(1001).fill(0);
    let min = 1000, max = 1, sum = 0;
    for (let p of skill) {
        freq[p]++;
        sum += p;
        min = Math.min(min, p);
        max = Math.max(max, p);
    }

    let teams = skill.length / 2;
    if (sum % teams != 0) {
        return -1;
    }

    let teamSum = sum / teams;
    let ans = 0;
    while (min < max) {
        if (min + max !== teamSum || freq[min] != freq[max]) {
            return -1;
        }
        ans += min * max * freq[min];
        min++;
        max--;
    }
    ans += (min === max && min + max === teamSum) ? freq[min] / 2 * min * max : 0;
    return ans;
};
```