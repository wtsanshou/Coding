# LC674. Longest Continuous Increasing Subsequence

### LeetCode

## Question

Given an unsorted array of integers, find the length of longest continuous increasing subsequence (subarray).

**Example 1:**

```
Input: [1,3,5,4,7]
Output: 3
```

**Explanation:** 

The longest continuous increasing subsequence is [1,3,5], its length is 3. 
Even though [1,3,5,7] is also an increasing subsequence, it's not a continuous one where 5 and 7 are separated by 4. 

**Example 2:**

```
Input: [2,2,2,2,2]
Output: 1
```

**Explanation:**

The longest continuous increasing subsequence is [2], its length is 1. 
**Note:** Length of the array will not exceed 10,000.

## Solutions

* C#1

```
public int FindLengthOfLCIS(int[] nums) {
        int maxLen = 1, res = 0;
        if(nums.Length == 1) return 1;
        for(int i=0; i<nums.Length-1; ++i){
            if(nums[i] < nums[i+1]){
                maxLen++;
            }
            else{
                maxLen = 1;
            }
            res = Math.Max(res, maxLen);
        }
        return res;
    }
```

## Explanation

**Corner Cases:**

1. nums is empty, return 0;
2. nums has only one number, return 1;
3. nums are all equal;
4. nums are descending order.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

