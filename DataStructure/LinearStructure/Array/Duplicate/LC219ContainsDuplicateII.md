# LC219. Contains Duplicate II

### LeetCode

## Question

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

## Solutions

### Solution 1

* C++ (32ms)
```
bool containsNearbyDuplicate(vector<int>& nums, int k) {
    unordered_map<int, int> count;
    for(int i=0; i<nums.size(); i++)
    {
        if(count[nums[i]] && i - count[nums[i]] < k) return true;
        count[nums[i]] = i+1;
    }
    return false;
}
```

* Java (19ms)
```
public boolean containsNearbyDuplicate(int[] nums, int k) {
    Map<Integer, Integer> match = new HashMap<Integer, Integer>();
    for(int i=0; i<nums.length; ++i)
    {
        if(match.containsKey(nums[i]) && (i-match.get(nums[i])) < k)
            return true;
        match.put(nums[i], i+1);
    }
    return false;
}
```

Using a `Map` to save the index of each number as `(number, index)`. If found a duplicated number, we can compare its index with current index.

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the size of the input `nums`.

## Follow up

* What if ask the absolute difference between i and j is `at least` k?

Then if found duplicated numbers, don't override their index value in the `Map`, keep the farest duplicated number in the `Map`.
