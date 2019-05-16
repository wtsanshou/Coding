# LC480. Sliding Window Median

### LeetCode

## Question

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

**Examples: **
```
[2,3,4] , the median is 3
[2,3], the median is (2 + 3) / 2 = 2.5
```

Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Your job is to output the median array for each window in the original array.

**For example,**
```
Given nums = [1,3,-1,-3,5,3,6,7], and k = 3.
Window position                Median
---------------               -----
[1  3  -1] -3  5  3  6  7       1
 1 [3  -1  -3] 5  3  6  7       -1
 1  3 [-1  -3  5] 3  6  7       -1
 1  3  -1 [-3  5  3] 6  7       3
 1  3  -1  -3 [5  3  6] 7       5
 1  3  -1  -3  5 [3  6  7]      6
Therefore, return the median sliding window as [1,-1,-1,3,5,6].
```

**Note: **

* You may assume k is always valid, ie: 1 ≤ k ≤ input array's size for non-empty array.

## Solutions

### Solution 1

* C++1 (1472ms)
```
vector<double> medianSlidingWindow(vector<int>& nums, int k) {
    vector<double> res;
    for(int i=0; i<=nums.size()-k; ++i)
    {
        vector<int> window(nums.begin()+i, nums.begin()+k+i);
        nth_element(window.begin(), window.begin()+k/2, window.end());
        double val = window[k/2]; 
        if(k % 2 ==0)
        {
            nth_element(window.begin(), window.begin()+(k-1)/2, window.end());
            val = (val + window[(k-1)/2])/2;
        }
        res.push_back(val);
    }
    return res;
}
```

Search all slides, using the `nth_element` to find the medians.

If using Java, you need to sort the elements in the sliding window every time.

**Complexity:**

* **worst-case time complexity:** O(N<sup>2</sup>), where `N` is length of `nums`.
* **worst-case space complexity:** `O(k)`.

### Solution 2

* C++2 (Might be very slow)
```
vector<double> medianSlidingWindow(vector<int>& nums, int k) {
    vector<double> res;
    vector<int> window(nums.begin(), nums.begin()+(k-1));
    for(int i=0; i<=nums.size()-k; ++i)
    { 
        window.push_back(nums[i]);
        sort(window.begin(), window.end());
        double val = window[k/2];
        
        if(k % 2 ==0)
        {
            val = (val + window[(k-1)/2])/2;
        }
        res.push_back(val);
        auto it = lower_bound(window.begin(), window.end(), nums[i-k+1]);
        window.erase(it);
    }
    return res;
}
```

1. Sort the sliding window.
2. Find median.
3. Add next element of the window
4. Erase the first element in the window.

**Complexity:**

* **worst-case time complexity:** O(N* k * log(k)), where `N` is length of `nums`.
* **worst-case space complexity:** `O(k)`.


### Solution 3

* C++3 (93ms) O(n*log(n))
```
vector<double> medianSlidingWindow(vector<int>& nums, int k) {
    vector<double> medians;
    multiset<int> window(nums.begin(), nums.begin()+k);
    auto mid = next(window.begin(), k/2);
    for(int i=k; ; ++i)
    {
        medians.push_back(((double)*mid + *prev(mid, 1-k%2)) / 2);
        if(i==nums.size()) return medians; 
        window.insert(nums[i]); 
        if(nums[i] < *mid) mid--; 
        if(nums[i-k] <= *mid) mid++; 
        window.erase(window.lower_bound(nums[i-k])); 
    }
    return medians;
}
```

Focus on the location of the median in the sliding window.

If add a element less than the median, move the locaiton of the median to left one step.

If add a element larger than the median, move the locaiton of the median to right one step.

**Complexity:**

* **worst-case time complexity:** O(N * log(N)), where `N` is length of `nums`.
* **worst-case space complexity:** `O(k)`.