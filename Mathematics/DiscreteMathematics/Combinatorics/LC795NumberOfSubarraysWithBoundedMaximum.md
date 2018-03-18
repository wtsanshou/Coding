# LC795. Number of Subarrays with Bounded Maximum

### LeetCode

## Question

We are given an array `A` of positive integers, and two positive integers `L` and `R` (`L <= R`).

Return the number of (contiguous, non-empty) subarrays such that the value of the maximum array element in that subarray is at least `L` and at most `R`.

**Example :**
```
Input: 
A = [2, 1, 4, 3]
L = 2
R = 3
Output: 3
Explanation: There are three subarrays that meet the requirements: [2], [2, 1], [3].
```

**Note:**

* L, R  and A[i] will be an integer in the range [0, 10^9].
* The length of A will be in the range of [1, 50000].

## Solutions

* Java1
```
class Solution {
    public int numSubarrayBoundedMax(int[] A, int L, int R) {
        int result = 0, lessThanR = 0, lessThanL=0;
        int lessThanLCombination = 0;
        for(int a : A){
            if(a <= R){
                lessThanR++;
                if(a >= L){
                    lessThanLCombination += getCombinationNumber(lessThanL);
                    lessThanL = 0;
                } 
            } 
            if(a < L) lessThanL++;
            if(a > R){
                lessThanLCombination += getCombinationNumber(lessThanL);
                result += getCombinationNumber(lessThanR) - lessThanLCombination;
                lessThanR = 0;
                lessThanL = 0;
                lessThanLCombination = 0;
            }
        }
        
        lessThanLCombination += getCombinationNumber(lessThanL);
        result += getCombinationNumber(lessThanR) - lessThanLCombination;
        
        return result;
    }
    
    private int getCombinationNumber(int length){
        return length * (length+1) / 2;
    }
}
```

## Explanation

The question is to get `the number of (contiguous, non-empty) subarrays such that the value of the maximum array element in that subarray is at least L and at most R.`

Reverse thinking: the above equals `the number of (contiguous, non-empty) subarrays such that the value of the maximum array element in that subarray is at most R.` minus `the number of (contiguous, non-empty) subarrays such that the value of the maximum array element in that subarray is less than L.`

* **worst-case time complexity:** `O(N)`, where `N` is the length of the input array `A`.
* **worst-case space complexity:** `O(1)`