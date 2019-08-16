# LC650. Two Keys Keyboard

### LeetCode

## Question

Initially on a notepad only one character 'A' is present. You can perform two operations on this notepad for each step:

**Copy All:** You can copy all the characters present on the notepad (partial copy is not allowed).

**Paste:** You can paste the characters which are copied last time.

Given a number n. You have to get exactly n 'A' on the notepad by performing the minimum number of steps permitted. Output the minimum number of steps to get n 'A'.

**Example 1:**
```
Input: 3
Output: 3
```

**Explanation:**

Intitally, we have one character 'A'.
In step 1, we use Copy All operation.
In step 2, we use Paste operation to get 'AA'.
In step 3, we use Paste operation to get 'AAA'.

**Note:**

* The n will be in the range [1, 1000].

## Solutions

* Java1
```
class Solution {
    
    private static int[] dp = new int[1001];
    
    public int minSteps(int n) {
        if(n==1) return 0;
        if(dp[n] != 0) return dp[n];
        for(int i=2; i<=n; ++i){
            if(dp[i] != 0) continue;
            for(int j=i/2; j>=1; --j){
                int step = i/j;
                if(step*j == i){
                    dp[i] = dp[j] + step;
                    break;
                }
            }
        }
        return dp[n];
    }
}
```

## Explanation

```
input   output
1       0
2       2
3       3
4       4
5       5
6       5 
7       7
8       6
9       6
10      7
11      11
12      7
.       .
.       .
.       .
```

From the input and output, we can see, if the input `n` can be divide exactly by a previous input number `x`, we can copy the result of `x` and paste it to get `n` A.

So, we need to find out the result of input `x` to get result of `n`. This is typical Dynamic Programming algorithm.

**Note:** Here, I used a static array to store the results. So, to calculate next input, we don't need to calculate previous results again.

* **worst-case time complexity:** O(n<sup></sup>)
* **worst-case space complexity:** O(n)