# LC442. Find All Duplicates in an Array

### LeetCode

## Question

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?

**Example:**
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```

## Solutions

### Solution 1

C++ (152ms)
vector<int> findDuplicates(vector<int>& nums) {
    vector<int> res;
    int n = nums.size();
    for(int num : nums)
    {
        int id = (num-1+n)%n;
        if(nums[id]<=0) res.push_back(id+1);
        else nums[id] -= n;
    }
    return res;
}

Similar question as <a href="LC448FindAllNumbersDisappearedInAnArray.md">LC448. Find All Numbers Disappeared in an Array</a>.

* **worst-case time complexity:** `O(N)`, where `N` is the size of the input `nums`.
* **worst-case space complexity:** `O(1)`