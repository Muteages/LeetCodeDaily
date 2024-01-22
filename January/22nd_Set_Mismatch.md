# Set Mismatch

https://leetcode.com/problems/set-mismatch

You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.


## Approach 

``` C++
    vector<int> findErrorNums(vector<int>& nums) {
        int n = nums.size();
        std::vector<int> unique(n + 1, 0);
        int duplicate = -1;
        int sum = 0;
        for (const int& num : nums)
        {
            if (unique[num] != 0)
            { // Find the duplicate number
                duplicate = num;
            }
            else
            {
                unique[num] = 1;
            }
            sum += num;
        }

        int exceptedSum = n * (n + 1) / 2;
        int missing = exceptedSum - (sum - duplicate);
        return {duplicate, missing};
    }
```