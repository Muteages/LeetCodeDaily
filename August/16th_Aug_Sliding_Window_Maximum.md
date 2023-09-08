# Sliding Window Maximum

https://leetcode.com/problems/sliding-window-maximum/description/

You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

## Approach 1
TLE if k is a large number.

``` C++
    int CurrentMax(std::vector<int>& nums, int st, int end)
    {
        int maxNum = INT_MIN;
        while (st <= end)
        {
            maxNum = std::max(nums[st], maxNum);
            st++;
        }
        return maxNum;
    }

    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        std::vector<int> ans;
        
        //First window
        // Or use std::max_element()  directly
        int maxNum = CurrentMax(nums, 0, k - 1);
        ans.emplace_back(maxNum);
        int PrevHead = 0;
        int i = k;
        while (i < nums.size())
        {
            if (nums[PrevHead] == maxNum)
            { // if the max number is out of the window, recalculate the max number
                // TLE if the k is a large number
                maxNum = CurrentMax(nums, PrevHead + 1, PrevHead + k);
            }
            else 
            {
                maxNum = std::max(maxNum, nums[i]);
            }
            ans.emplace_back(maxNum);
            i++;
            PrevHead++;
        }
        return ans;
    }
```


## Approach 2 
Use max-heap std::priority_queue

``` C++
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        std::vector<int> ans;
        std::priority_queue<std::pair<int, int>> pq; //val - index

        for (int i = 0; i < k; i++)
        {
            pq.push(std::make_pair(nums[i], i));
        }
        ans.emplace_back(pq.top().first);

        int prevHead = 0; // record the previous head
        while (k < nums.size())
        {
            while (!pq.empty() && prevHead >= pq.top().second)
            { // pop up elements which run out of the window
                pq.pop();
            }

            pq.push(std::make_pair(nums[k], k));
            ans.emplace_back(pq.top().first);
            k++;
            prevHead++;
        }
        return ans;
    }
```

## Approach 3
Maintain a deque to store the indices.

``` C++
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        std::vector<int> ans;

        std::deque<int> dq; // store indices of potential max numbers
        for (int i = 0; i < nums.size(); i++)
        {
            while (!dq.empty() && nums[dq.back()] <= nums[i])
            { // remove numbers which are smaller than current number
                dq.pop_back();
            }
            dq.emplace_back(i);  

            if (dq.front() <= i - k) 
            { // remove the number if it runs out of the window
                dq.pop_front();
            }

            if (i >= k - 1)
            { 
                ans.emplace_back(nums[dq.front()]);
            }

        }
        return ans;
    }
```
