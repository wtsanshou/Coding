# LC334. Increasing Triplet Subsequence

### LeetCode

## Question

Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:

Return true if there exists i, j, k 

such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.

Your algorithm should run in O(n) time complexity and O(1) space complexity.

**Examples:**
```
Given [1, 2, 3, 4, 5],
return true.
Given [5, 4, 3, 2, 1],
return false.
```

## Solutions

### Solution 1

* C++ (12ms)
```
bool increasingTriplet(vector<int>& nums) {
    if(nums.size()<3) return false;
    set<int> s;
    for(int n : nums)
    {
        if(s.find(n) != s.end()) continue;
        s.insert(n);
        auto it = s.upper_bound(n);
        if(it != s.end()) s.erase(it);
        if(s.size() == 3) return true;
    }
    return false;
}
```

Using a `set` to store the possible increasing subsequence. Traversal the `nums`, only keep the numbers who is less than the current number. If get 3 numbers in the set, it means a increasing subsequence is existed.

**For example:**

`3  6   2   4   1   5`

numbers in set
```
3
3   6
2   6
2   4
1   4
1   4   5
```

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`

### Solution 2 

* C++ (6ms)
```
bool increasingTriplet(vector<int>& nums) {
    vector<int> res(2, INT_MAX);
    for(auto num : nums)
    {
        if(num <= res[0]) res[0] = num;
        else if(num <= res[1]) res[1] = num;
        else return true;
    }
    return false;
}
```

Using an array to store the first two numbers of increasing subsequence. Traversal the array, update the first two numbers (remove the upper bound). If found a number bigger than the first two numbers, it means a increasing subsequence is existed.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`
