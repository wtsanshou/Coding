# LC350. Intersection of Two Arrays II 

### LeetCode

## Question

Given two arrays, write a function to compute their intersection.

**Example:**
```
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].
```

**Note:**

* Each element in the result should appear as many times as it shows in both arrays.
* The result can be in any order.

**Follow up:**

* What if the given array is already sorted? How would you optimize your algorithm?
* What if nums1's size is small compared to nums2's size? Which algorithm is better?
* What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

## Solutions

### Solution 1

* C++ (9ms)
```
vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
    vector<int> res;
    unordered_map<int, int> counts;
    for(int num1 : nums1)
        counts[num1]++;
    for(int num2 : nums2)
        if(counts[num2]-- > 0)
            res.push_back(num2);
    return res;
}
```

Using a `map` to count the numbers in `nums1`. Check in `nums2`, find all duplicated in the `map`.

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums1` and `nums2`.
* **worst-case space complexity:** `O(N)`, where `N` is the size of the input `nums1` and `nums2`.

### Solution 2

* C++ (6ms)
```
vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
    vector<int> res;
    sort(nums1.begin(), nums1.end());
    sort(nums2.begin(), nums2.end());
    int i=0, j=0, len1=nums1.size(), len2=nums2.size();
    while(i<len1 && j<len2)
    {
        if(nums1[i] == nums2[j])
        {
            res.push_back(nums1[i]);
            i++;
            j++;
        }
        else if(nums1[i] > nums2[j]) j++;
        else i++;
    }
    return res;
}
```

Sort both `nums1` and `nums2`, find duplicated numbers from left to right.

* **worst-case time complexity:** `O(N*log(N))`, where `N` is the size of the input `nums1` and `nums2`.
* **worst-case space complexity:** `O(log(N))`, where `N` is the size of the input `nums1` and `nums2`.