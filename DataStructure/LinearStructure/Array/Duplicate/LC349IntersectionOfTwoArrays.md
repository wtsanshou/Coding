# LC349. Intersection of Two Arrays

### LeetCode

## Question

Given two arrays, write a function to compute their intersection.

**Example:**
```
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].
```

**Note:**
* Each element in the result must be unique.
* The result can be in any order.

## Solutions

### Solution 1

* C++ (9ms)
```
vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
    set<int> set;
    vector<int> res;
    for(int num : nums1)
        set.insert(num);
    for(int num : nums2)
    {
        if(set.count(num)>0)
        {
            res.push_back(num);
            set.erase(num);
        }
    }
    return res;
}
```

* Java (6ms)
```
public int[] intersection(int[] nums1, int[] nums2) {
    HashSet<Integer> sta1 = new HashSet();
    HashSet<Integer> sta2 = new HashSet();
    for(int n1 : nums1)
    {
        sta1.add(n1);
    }
    for(int n2 : nums2)
    {
        if(sta1.contains(n2)) sta2.add(n2);
    }
    int[] res = new int[sta2.size()];
    int i=0;
    for(Integer n : sta2) res[i++] = n;
    return res;
}
```

Put `nums1` into `set1`, then use `set2` to find `nums2`'s numbers which appears in `set1`.

* **worst-case time complexity:** `O(N)`, where `N` is the length of the `nums1` and `nums2.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the `nums1` and `nums2.



