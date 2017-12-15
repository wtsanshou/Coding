# LC398. Random Pick Index

### LeetCode

## Question

Given an array of integers with possible duplicates, randomly output the index of a given target number. You can assume that the given target number must exist in the array.

**Note:**

The array size can be very large. Solution that uses too much extra space will not pass the judge.

**Example:**

`int[] nums = new int[] {1,2,3,3,3};`

`Solution solution = new Solution(nums);`

// pick(3) should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.

`solution.pick(3);`

// pick(1) should return 0. Since in the array only nums[0] is equal to 1.

`solution.pick(1);`

## Solutions

* C++1 (146ms)
```
class Solution {
private: 
    vector<int> myNums;
public:
    Solution(vector<int> nums) {
        myNums = nums;
    }
    
    int pick(int target) {
        int res = -1, count=0;
        for(int i=0; i<myNums.size(); ++i)
            if(myNums[i] == target && (rand() % ++count == 0))
                res = i;
        return res;
    }
};
```

## Explanation

As explained in <a href="https://en.wikipedia.org/wiki/Harmonic_series_(mathematics)">Harmonic series</a>, to get the equal probability, we need to travel the array and count the target. For each target index, it has `1/count` probability to be the result.

![HarmonicSeries](Images/HarmonicSeries.tiff)

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)
