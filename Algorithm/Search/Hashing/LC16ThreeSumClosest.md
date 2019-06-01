# LC16. Three Sum Closest

### LeetCode

## Question

Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**For example** 
```
given array S = {-1 2 1 -4}, and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

## Solutions

### Solution 1

* C++
```
int threeSumClosest(vector<int>& nums, int target) {
    sort(nums.begin(), nums.end());
    int closest = nums[0] + nums[1] + nums[2];
    int n = nums.size();
    for(int k=0; k<n-2; ++k)
    {
        int i=k+1, j=n-1;
        while(i<j)
        {
            int x = nums[k] + nums[i] + nums[j];
            if(abs(x-target) < abs(closest-target))
            {
                closest = x;
                if(x == target) return target;
            }
            if(x > target) j--;
            else i++;
        }
    }
    return closest;
}
```

1. Sort the `nums`
2. Based on the first element in the triplet, check if there is a closer triplet to the target.

Skip duplicated numbers could be faster.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of the input `nums`.
