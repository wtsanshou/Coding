# LC90. Subsets II

### LeetCode

## Question

Given a collection of integers that might contain duplicates, nums, return all possible subsets.

**Note:** The solution set must not contain duplicate subsets.

**For example**
```
If nums = [1,2,2], a solution is:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    void CollectSubsets(vector<vector<int>>& res, vector<int> aRow, int start, vector<int> nums)
    {
        if(start >= nums.size()) return;
        for(int i=start; i<nums.size(); ++i)
        {
            if(i!=start && nums[i]==nums[i-1]) continue;
            aRow.push_back(nums[i]);
            res.push_back(aRow);
            CollectSubsets(res, aRow, i+1, nums);
            aRow.pop_back();
        }
    }
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> aRow;
        res.push_back(aRow);
        sort(nums.begin(), nums.end());
        CollectSubsets(res, aRow, 0, nums);
        return res;
    }
};
```

Using `back tracking`. To avoid duplicate subsets, we need to sort the `nums`, and skip the equal numbers during `back tracking`.

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.

### Solution 2

* C++
```vector<vector<int>> subsetsWithDup(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    vector<vector<int>> res(1, vector<int>());
    vector<int> aRow;
    int size = 1;
    for(int i=0; i<nums.size(); ++i)
    {
        int start = (i>0)&&(nums[i]==nums[i-1]) ? size : 0;
        size = res.size();
        for(int j=start; j<size; ++j)
        {
            res.push_back(res[j]);
            res.back().push_back(nums[i]);
        }
    }
    return res;
}
```

Iteration way

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.