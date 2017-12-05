# LC213. House Robber II

### LeetCode

## Question

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

## Solutions

* C++1
```
class Solution {
public:
    int robHelper(vector<int>& nums, int start, int end)
    {
        int cur, pre=0, bpre = 0;
        for(int i=start; i<=end; ++i)
        {
            cur = max(pre, bpre+nums[i]);
            bpre = pre;
            pre = cur;
        }
        return max(pre, bpre);
    }

    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n<2) return n? nums[0]:0;
        return max(robHelper(nums, 0, n-2), robHelper(nums, 1, n-1));
    }
};
```

* C++2
```
class Solution {
public:
    int maxRob(vector<int>& nums, int start, int end)
    {
        if(start>end) return 0;
        int prepre=0, pre=nums[start];
        for(int i=start+1; i<end; ++i)
        {
            int cur = prepre+nums[i];
            prepre = pre;
            pre = max(pre, cur);
        }
        return max(pre, prepre);
    }

    int rob(vector<int>& nums) {
        return max(maxRob(nums, 0, nums.size()-1), maxRob(nums, 1, nums.size()));
    }
};
```

## Explanation

1. Rob from 0<sup>th</sup> to (n-2)<sup>th</sup>;
2. Rob from 1<sup>th</sup> to (n-1)<sup>th</sup>;
3. The larger amount of money of the above two is the result.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)
