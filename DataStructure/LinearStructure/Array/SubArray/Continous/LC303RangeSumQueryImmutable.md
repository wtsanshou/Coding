#LC303. Range Sum Query – Immutable

### LeetCode

## Question

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

**Example:**
```
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

**Note:**

* 1.  You may assume that the array does not change.
* 2.  There are many calls to sumRange function.

## Solutions

```
/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(i,j);
 */
```

* C++1 (206ms) write O(n) read O(1)
```
class NumArray {
private:
    vector<int> sumLeft;
public:
    NumArray(vector<int> nums) {
        int n = nums.size();
        sumLeft.resize(n+1,0);
        int left=0;
        for(int i=0; i<n; ++i)
        {
            sumLeft[i] = left;
            left += nums[i];
        }
        sumLeft[n] = left;
    }
    int sumRange(int i, int j) {
        return sumLeft[j+1] - sumLeft[i];
    }
};
```

* C++2 (28ms) write O(n) read O(1)
```
class NumArray {
public:
    vector<int> numsM;
    NumArray(vector<int> &nums) {
        int n = nums.size();
        numsM.resize(n+1);
        for(int i=0; i<n; ++i)
            numsM[i+1] = numsM[i] + nums[i];
    }
    int sumRange(int i, int j) {
        return numsM[j+1] - numsM[i];
    }
};
```

* C++3 (28ms) write O(n) read O(1)
```
class NumArray {
private:
    vector<int> numsM;
public:
    NumArray(vector<int> &nums) {
        numsM.push_back(0);
        for(int n : nums)
        {
            numsM.push_back(numsM.back()+n);
        }
    }
    int sumRange(int i, int j) {
        return numsM[j+1] - numsM[i];
    }
};
```

* Java1 (3ms) write O(n) read O(1)
```
public class NumArray {
    private int[] sums; 
    public NumArray(int[] nums) {
        int n = nums.length;
        sums = new int[n+1];
        for(int i=0; i<n; ++i)
            sums[i+1] = nums[i] + sums[i];
    }
    public int sumRange(int i, int j) {
        return sums[j+1] - sums[i];
    }
}
```

## Explanation

Using an array `sums` to save the sum of all left numbers of position `i`.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.
