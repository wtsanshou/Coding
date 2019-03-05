# LC217. Contains Duplicate

### LeetCode

## Question

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

## Solutions

### Solution 1

* Java (6ms)
```
public boolean containsDuplicate(int[] nums) {
    Arrays.sort(nums);
    for(int i=1; i<nums.length; ++i)
        if(nums[i] == nums[i-1]) return true;
    return false;
}
```

Sort the array `nums`, duplicated number will be adjacent if has.

* **worst-case time complexity:** `O(N*log(N))`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(log(N))`, where `N` is the size of the input `nums`.

### Solution 2

* C++1 (48ms)
```
bool containsDuplicate(vector<int>& nums) {
    unordered_map<int, int> counts;
    int len = nums.size();
    for(int i=0; i<len; i++)
    {
        if(++counts[nums[i]]>1)
            return true;
    }
    return false;
}
```

* C++2 (66ms)
```
bool containsDuplicate(vector<int>& nums) {
    if(nums.empty()) return false;
    set<int> set;
    for(int num : nums)
    {
        if(set.count(num)>0) return true;
        set.insert(num);
    }
    return false;
}
```

* Java (9ms)
```
public boolean containsDuplicate(int[] nums) {
    Set<Integer> set = new HashSet();
    for(int num : nums)
        if(!set.add(num)) return true;
    return false;
}
```

Using `Set` or `Map` to save unique numbers. If has duplicated number, it can be found in the `Set` or `Map`.

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(N)`, where `N` is the size of the input `nums`.
