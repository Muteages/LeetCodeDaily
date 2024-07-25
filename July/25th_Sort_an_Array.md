# Sort an Array

https://leetcode.com/problems/sort-an-array

Given an array of integers nums, sort the array in ascending order and return it.

You must solve the problem without using any built-in functions in O(nlog(n)) time complexity and with the smallest space complexity possible.

## Approach 1

Counting sort

``` C++
    vector<int> sortArray(vector<int>& nums) {
        std::map<int, int> freq;
        for (int num : nums)
        {
            freq[num]++;
        }
        
        int idx = 0;
        for (auto& [num, f] : freq)
        {
            while (f--)
            {
                nums[idx++] = num;
            }
        }
        return nums;
    }
```

## Approach 2

Quick sort with the "randomise" pivot

``` C++
    void quickSort(std::vector<int>& nums, int left, int right)
    {
        // if (left >= right) return;

        // int pivot = partition(nums, left, right);
        // quickSort(nums, left, pivot - 1);
        // quickSort(nums, pivot + 1, right);
        while (left < right)
        {
            int pivot = partition(nums, left, right);
            if (pivot - left < right - pivot)
            {
                quickSort(nums, left, pivot - 1);
                left = pivot + 1;
            }
            else
            {
                quickSort(nums, pivot + 1, right);
                right = pivot - 1;
            }
        }
    }

    int partition(std::vector<int>& nums, int left, int right)
    {
        int med = median(nums, left, right, left + (right - left) / 2); // Get "Random" pivot"
        std::swap(nums[left], nums[med]);
        int i = left, j = right, pivot = nums[left];
        while (i < j)
        {
            while (i < j && nums[j] >= pivot)
            {
                j--;
            }
            while (i < j && nums[i] <= pivot)
            {
                i++;
            }
            std::swap(nums[i], nums[j]);
        }
        std::swap(nums[i], nums[left]);
        return i;
    }

    int median(std::vector<int>& nums, int left, int right, int mid)
    { 
        int l = nums[left], r = nums[right], m = nums[mid];
        if ((l <= m && m <= r) || (r <= m && m <= l))
        { // mid is the median number
            return mid;
        }
        else if ((m <= l && l <= r) || (r <= l && l <= m))
        { // left is the median number
            return left;
        }
        return right;
    }


    vector<int> sortArray(vector<int>& nums) {
        quickSort(nums, 0, nums.size() - 1);
        return nums;
    }
```

## Approach 3

Merge sort

``` C++
    void mergeSort(std::vector<int>& nums, std::vector<int>& buffer, int left, int right)
    {
        if (left >= right) return;
        int mid = left + (right - left) / 2;
        mergeSort(nums, buffer, left, mid);
        mergeSort(nums, buffer, mid + 1, right);
        merge(nums, buffer, left, mid, right);
    }

    void merge(std::vector<int>& nums, std::vector<int>& buffer, int left, int mid, int right)
    {
        int i = left, j = mid + 1, bufferIdx = left;
        while(i <= mid && j <= right)
        {
            if (nums[i] <= nums[j])
            {
                buffer[bufferIdx++] = nums[i++];
            }
            else
            {
                buffer[bufferIdx++] = nums[j++];
            }
        }

        while (i <= mid)
        {
            buffer[bufferIdx++] = nums[i++];
        }
        while (j <= right)
        {
            buffer[bufferIdx++] = nums[j++];
        }

        for (int i = left; i < bufferIdx; i++)
        {
            nums[i] = buffer[i];
        }
    }
    vector<int> sortArray(vector<int>& nums) {
        int n = nums.size();
        std::vector<int> buffer(n, 0);
        mergeSort(nums, buffer, 0, n - 1);
        return nums; 
    }
```

``` JavaScript
var sortArray = function(nums) {
    const n = nums.length;
    const buffer = Array(n).fill(0);

    const mergeSort = (left, right) => {
        if (left >= right) return;
        let mid = Math.floor((left + right) / 2);
        mergeSort(left, mid);
        mergeSort(mid + 1, right);
        merge(left, mid, right);
    }

    const merge = (left, mid, right) => {
        let i = left, j = mid + 1, idx = left;
        while (i <= mid && j <= right) {
            if (nums[i] <= nums[j]) {
                buffer[idx++] = nums[i++];
            }
            else {
                buffer[idx++] = nums[j++];
            }
        }
        // Fill the remaining elements
        while (i <= mid) {
            buffer[idx++] = nums[i++];
        }
        while (j <= right) {
            buffer[idx++] = nums[j++];
        }

        for (let i = left; i < idx; i++) {
            nums[i] = buffer[i];
        }
    }
    mergeSort(0, n - 1);
    return nums;
};
```