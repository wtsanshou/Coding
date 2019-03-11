# LC47. Permutations II

### LeetCode

## Question

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

**For example**
```
[1,1,2] have the following unique permutations:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    void permuteDFS(vector<vector<int>>& res, vector<int> nums, int start)
    {
        if(start==nums.size()-1)
        {
            res.push_back(nums);
            return;
        }
        for(int i=start; i<nums.size(); ++i)
        {
            if(i!=start && nums[i]==nums[start]) continue;
            swap(nums[i], nums[start]);
            permuteDFS(res, nums, start+1);
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        permuteDFS(res, nums, 0);
        return res;
    }
};
```

The solution is to sort the input array `nums` first. Then DFS from the first number and skip the duplicated numbers.

* **worst-case time complexity:** O(N<sup>2</sup>), where `N` is the length of the input `nums`.
* **worst-case space complexity:** O(N<sup>2</sup>), where `N` is the length of the input `nums`.
