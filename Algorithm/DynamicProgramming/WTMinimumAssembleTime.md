# WT. Minimum Assemble Time

## Question

Given n components, indexed from 0 to n-1. Each component has a size which is represented by the integer in the array. 

A worker can only combine two components at a time. The time required to put two components together is equal to the sum of the components' size. 

Your task is to find the minimum possible time to combine all components together.

**Note**

* 2<= `n` <= 10<sup>6</sup>
* 0 < `input[i]` <= 10<sup>6</sup>

**Example 1**

```
Input:
[8,4,6,12]

Return:
58

Explanation:
8,4,6,12 
8, 10,12 -> 10
18,   12 -> 10 + 18 = 28
    30   -> 28 + 30 = 58
```

**Example 2**

```
Input:
[8,4,6,12,2,3]

Return:
85
```

## Solutions

### Solution 1

* Java
```
public int minPossibleTimes(int[] input){
     int n = input.length;
     int[][] dp = new int[n][n];
     for(int i=0; i<n; i++){
         Arrays.fill(dp[i], Integer.MAX_VALUE);
         dp[i][i] = 0;
     }
     
     int[][] sumDp = new int[n][n];
     for(int i=0; i<n; i++){
         for(int j=i; j<n; j++){
             for(int k=i; k<=j; k++){
                 sumDp[i][j]+=input[k];
             }
         }
     }
     
     for(int len=1; len<n; len++){
         for(int left=0; left<n-len; left++){
             for(int mid=left+1; mid<=left+len; mid++){
                 int right = left+len;
                 int min = sumDp[left][right]+dp[left][mid-1]+ dp[mid][right];
                 dp[left][right] = Math.min(dp[left][right], min);
             }
         }    
     }
     
     return dp[0][n-1];
 }
```

When I get this question, I realized it's a dynamic programming problem. The key is how to divide the problem to smaller problems.

We can assume we already have the result in `dp[0][n-1]` which should be generate by it's children results.

Let's see the example:

```
8,4,6,12 
8, 10,12 -> 10
18,   12 -> 10 + 18 = 28
    30   -> 28 + 30 = 58
```

We can see one child result is the sum of that children group:

```
4+6      = 10
8+4+6    = 18
8+4+6+12 = 30
```

So the `dp[i][j]` must equal to `sum[i][j] + something`

Normally the `something` is a combination of its children `dp`. Based on the question, the combination should be the sum of two children `dp`.

Let's see the example again, and add more information:

```
8,4,6,12 
8, 10,12 -> 0+0 +  10 = dp[1][1] + dp[2][2] + sum[1][2] = dp[1][2] = 10
18,   12 -> 0+10 + 18 = dp[0][0] + dp[1][2] + sum[0][2] = dp[0][2] = 28
    30   -> 28+0 + 30 = dp[0][2] + dp[3][3] + sum[0][3] = dp[0][2] = 58
```

It's clear now: `dp[i][j] = dp[i][mid] + dp[mid+1][j] + sum[i][j]`. A trick part here is `dp[i][i]=0`.

**Complexity:**

* **worst-case time complexity:** O(n<sup>3</sup>), where `n` is the length of `input`.
* **worst-case space complexity:** O(n<sup>2</sup>), where `n` is the length of `input`.
