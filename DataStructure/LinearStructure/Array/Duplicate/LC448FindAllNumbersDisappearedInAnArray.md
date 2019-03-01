# LC448. Find All Numbers Disappeared in an Array

### LeetCode

## Question

Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

**Follow up**

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

**Example:**
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

## Solutions

### Solution 1

* Java
```
public int[] findDisappearedNumbers(int[] nums){
    int n = nums.length;
    boolean[] map = new boolean[n+1];
    for(int num : nums)
        map[num] = true;
    List<Integer> res = new ArrayList<>();
    for(int i=1; i<map.length; ++i)
        if(!map[i])
            res.add(i);
    return res.toArray(new Integer[res.size()]);
}
```

Using `Bucket Sort` to sort the `nums`. The disappeared numbers will not be in bucket `map`. But it uses extra space.

* **worst-case time complexity:** O(N), where `N` is the length of the `nums`.
* **worst-case space complexity:** O(N), where `N` is the length of the `nums`.

### Solution 2

* C++ (142ms) 
```
vector<int> findDisappearedNumbers(vector<int>& nums) {
    int n = nums.size();
    for(auto num : nums)
    {
        int id = (num-1+n)%n;
        if(nums[id] > 0)
            nums[id] -= n;
    }
    vector<int> res;
    for(int i=1; i<=n; ++i)
    {
        if(nums[i-1] > 0)
            res.push_back(i);
    }
    return res;
}
```

`(num-1+n)%n` will always point to the same location in the `nums`, no matter how many times `nums[id] -= n`. So all appeared numbers in the `nums` will be negative.

* **worst-case time complexity:** O(N), where `N` is the length of the `nums`.
* **worst-case space complexity:** O(1).

