# LC697. Degree of an Array

### LeetCode

## Question

Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums.

**Example 1:**

```
Input: [1, 2, 2, 3, 1]
Output: 2
```

**Explanation:**

The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:

```
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
```

The shortest length is 2. So return 2.

**Example 2:**

```
Input: [1,2,2,3,1,4,2]
Output: 6
```

**Note:**

* nums.length will be between 1 and 50,000.
* nums[i] will be an integer between 0 and 49,999.

## Solutions

* Java1

```
class Solution {
    public int findShortestSubArray(int[] nums) {
        int maxFreq = 0;
        Map<Integer, NumDegree> map = new HashMap<>();
        for(int i=0; i<nums.length; ++i){
            if(map.containsKey(nums[i])){
                map.get(nums[i]).increaseFreq();
                map.get(nums[i]).countDistance(i);
            }
            else{
                map.put(nums[i], new NumDegree(1, i, 1));
            }
            maxFreq = Math.max(maxFreq, map.get(nums[i]).getFreq());
        }
        
        int res = 50_000;
        if(maxFreq == 1) return 1;
        for(Integer key : map.keySet()){
            NumDegree dNum = map.get(key);
            if(maxFreq == dNum.getFreq())
                res = Math.min(res, dNum.getDistance());
        }
        return res;
    }
}

class NumDegree{
    private int freq;
    private int left;
    private int distance;
    public NumDegree(int freq, int left, int distance){
        this.freq = freq;
        this.left = left;
        this.distance = distance;
    }
    public void increaseFreq(){
        freq += 1;
    }
    public void countDistance(int right){
        distance = right - left + 1;
    }
    public int getFreq(){
        return freq;
    }
    public int getDistance(){
        return distance;
    }
}
```

## Explanation

1. Count the maximum frequency (might be more than one number)
2. Count the distance between the current number `x` and the first same number `x`.
3. Check all numbers with the maximum frequency. Find the minmum distance from them.

**Corner Cases:**

1. maxFreq == 1
2. more than one number with the maximum frequency.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)