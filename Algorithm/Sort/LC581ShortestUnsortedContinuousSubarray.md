# LC581. Shortest Unsorted Continuous Subarray

### LeetCode

## Question

Given an integer array, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the shortest such subarray and output its length.

**Example 1:**
```
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
```

**Note:**

1.	Then length of the input array is in range [1, 10,000].
2.	The input array may contain duplicates, so ascending order here means <=.

## Solutions

### Solution 1

* C++
```
int findUnsortedSubarray(vector<int>& nums) {
    vector<int> sorted(nums);
    sort(sorted.begin(), sorted.end());
    int i=0, n=nums.size();
    for(; i<n; ++i)
        if(nums[i]!=sorted[i]) break;
    int j=n-1;
    for(; j>i; --j)
        if(nums[j]!=sorted[j]) break;
    return i==j ? 0 : j-i+1;
}
```

The idea is to get a sorted version of the `nums` first. Then compare the sorted and the unsorted to find out the different starting point and the ending point.

* **worst-case time complexity:** O(N*log(N)), where `N` is the length of the `nums`.
* **worst-case space complexity:** O(N), where `N` is the length of the `nums`.
