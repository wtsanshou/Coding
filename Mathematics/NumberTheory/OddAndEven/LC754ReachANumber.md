# LC754. Reach a Number

### LeetCode

## Question

You are standing at position 0 on an infinite number line. There is a goal at position target.

On each move, you can either go left or right. During the n-th move (starting from 1), you take n steps.

Return the minimum number of steps required to reach the destination.

**Example 1:**
```
Input: target = 3
Output: 2
Explanation:
On the first move we step from 0 to 1.
On the second step we step from 1 to 3.
```

**Example 2:**
```
Input: target = 2
Output: 3
Explanation:
On the first move we step from 0 to 1.
On the second move we step  from 1 to -1.
On the third move we step from -1 to 2.
```

**Note:**

* target will be a non-zero integer in the range [-10^9, 10^9].

## Solutions

* Scala1
```
object Solution {
    def reachNumber(target: Int): Int = {
        val n = Math.abs(target)
        var res = (Math.sqrt(n.toDouble * 2 +0.25)-0.5).toInt
        if(sumUpTo(res) == n) return res
        res = res + 1
        while((sumUpTo(res) - n) %2 != 0){
            res = res + 1
        }
        res
    }
    
    def sumUpTo(n: Int): Int = {
        n*(n+1)/2
    }
}
```

* Java
```
public class Solution {
    /**
     * @param target: the destination
     * @return: the minimum number of steps
     */
    public int reachNumber(int target) {
        int n = Math.abs(target);
        int res = (int)(Math.sqrt((double)n * 2 + 0.25) - 0.5);
        int sum = sumTo(res);
        if (sum == n) return res;
        
        res++;
        while ((sumTo(res) - n) % 2 != 0) {
            res++;
        }
        
        return res;
    }
    
    private int sumTo(int n) {
        return n * (n + 1) / 2;
    }
    
}
```

## Explanation

To solve this kind of question, we need to list some input and output to find some clue.

```
*   *       *           *               *        *          * 
0   1   2   3   4   5   6   7   8   9   10   ... 15   ...   21  ...
0   1   3   2   3   5   3   5   4   5   4   ...
```

`*` mark all the maximum distance of n-move.

To reach a positive number `n`, we need to `sum(+-0, +-1, +-2, +-3, ..., +-n)`. The minimum number of steps requires only one `-` in the `sum`; Inversely, To reach a negative number `n`, the minimum number of steps requires only one `+` in the `sum`.

For example

```
  1 + 2 + 3 + ... -x + (x+1) + ... + n
= n*(n+1)/2  -x   -x
= n*(n+1)/2 - 2*x
= target
```

The result is `n*(n+1)/2 - 2*x`, where `x` is the number with reversed sign. Therefore `n*(n+1)/2 - target` == `2*x` == `even`.

Corner case: `n*(n+1)/2 == target`

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(1)

