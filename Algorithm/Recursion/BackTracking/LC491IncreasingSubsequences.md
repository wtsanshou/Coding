# LC491. Increasing Subsequences

### LeetCode

## Question

Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2 .

**Example:**
```
Input: [4, 6, 7, 7]
Output: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
```

**Note:**
1. The length of the given array will not exceed 15.
2. The range of integer in the given array is [-100,100].
3. The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.

## Solutions

### Solution 1

* C++ (296ms)
```
class Solution {
public:
    void backTracking(vector<vector<int>>& res, vector<int>& sub, vector<int>& nums, int start, int end)
    {       
        if(sub.size()>=2) res.push_back(sub);
        unordered_map<int, int> map;
        for(int i=start; i<end; ++i)
        {
            if(map[nums[i]] > 0) continue; // the same nums[i], the same size of sub should only appare once.
            if(sub.size()==0 || nums[i]>=sub.back())
            {
                map[nums[i]]++;
                sub.push_back(nums[i]);
                backTracking(res, sub, nums, i+1, end);
                sub.pop_back();
            }
        }
    }
    vector<vector<int>> findSubsequences(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> sub;
        backTracking(res, sub, nums, 0, nums.size());
        return res;
    }
};
```

Typical `Back tracking`, be careful the corner cases:

1. Avoid duplicated sub array.
2. The first element in the sub array.

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** O(n<sup>2</sup>), where `n` is the length of the `nums`.

