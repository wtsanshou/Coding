# Lint1753. Doing Homework

### LintCode

## Question

For n people, each of them needs to do m jobs independently.
The i job takes cost[i] time. Since each person's free time is different, the i person has val[i] time, which means that the total time for his jobs will not exceed val[i]. Everyone starts with the first job, then the 2nd, the 3rd... Now, you need to figure out how much time they spend.

**Example 1:**
```
Given `cost=[1,2,3,5]`,`val=[6,10,4]`, return `15`.

Input:
[1,2,3,5]
[6,10,4]

Output:
15

Explanation:
The first person can complete the 1st job, the 2nd job, the 3rd job, 1+2+3<=6.
The second person cancomplete the 1st job, the 2nd job, the 3rd job, and cannot complete the 4th job, 1+2+3<=10, 1+2+3+5>10.
The third person can complete  the 1st job, the 2nd job, and cannot complete the 3rd job,  1+2<=4, 1+2+3>4.
1+2+3+1+2+3+1+2=15, returning 15.
```

**Example 2:**

```
Given `cost=[3,7,3,2,5]`,`val=[10,20,12,8,17,25]`, return `78`.

Input:
[3,7,3,2,5]
[10,20,12,8,17,25]

Output:
78

Explanation:
The first person can complete the 1st job, the 2nd job, 3 + 7<=10.
The second person cancomplete the 1st job, the 2nd job, the 3rd job, the 4th job,the 5th job, 3+7+3+2+5<=20
The third person can complete  the 1st job, the 2nd job, and cannot complete the 3rd job,  3+7<=12,3+7+3>12.
The forth person can complete  the 1st job, and cannot complete the 2nd job,  3<=8,7+3>8.
The fifth person can complete  the 1st job, the 2nd job, the 3rd job, the 4th job, and cannot complete the 5th job,3+7+3+2<=17,3+7+3+2+5>17.
The sixth person cancomplete the 1st job, the 2nd job, the 3rd job, the 4th job,the 5th job, 3+7+3+2+5<=25
3+7+3+7+3+2+5+3+7+3+3+7+3+2+3+7+3+2+5=78, returning 78.
```

**Notice**

* 1<=n<=100000
* 1<=m<=100000
* 1<=val[i]<=100000
* 1<=cost[i]<=100000

## Solutions

### Solution 1

* Java
```
public long doingHomework(int[] cost, int[] val) {
    TreeSet<Long> set = new TreeSet<>();
    set.add(0L);
    for (int i = 0; i < cost.length; i++) {
        set.add(set.last() + cost[i]);
    }
    
    long res = 0;
    for (int value : val) {
        res += set.floor((long)value);
    }
    
    return res;
}
```

For this question, we can pre-process the `cost` to get prefix sums. So that we don't need to re-calculate the total costs for each person.

With the prefix sums, we can do floor binary search for each person's value. I did not came out the floor binary search in that short time. But I know `TreeSet` has this `floor` feature. So I just add theos prefix sums into a `TreeSet` and do floor for each person.

**Complexity:**

* **worst-case time complexity:** `O(log(n) * m)`, where `n` is the length of the input `cost`, `m` is the length of `val`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `cost`.

### Solution 2

* Java
```
public class Solution {
    /**
     * @param cost: the cost
     * @param val: the val
     * @return: the all cost
     */
    public long doingHomework(int[] cost, int[] val) {
        int n = cost.length;
        long[] sumCost = new long[n + 1];
        for (int i = 0; i < n; i++) {
            sumCost[i + 1] = sumCost[i] + cost[i];
        }
        
        long res = 0L;
        for (int value : val) {
            res += binarySearchFloor(sumCost, value);
        }
        
        return res;
    }
    
    private long binarySearchFloor(long[] sumCost, long target) {
        int i = 0, j = sumCost.length - 1;
        while (i < j) {
            int mid = i + (j - i) / 2;
            if (mid < sumCost.length - 1 && sumCost[mid] <= target && target < sumCost[mid + 1])    
                return sumCost[mid];
            if (mid > 0 && sumCost[mid - 1] <= target && target < sumCost[mid])
                return sumCost[mid - 1];
            
            if (sumCost[mid] < target)
                i = mid + 1;
            else
                j = mid - 1;
        }
        return sumCost[i];
    }
}
```

It's a good chance to figure out how to implement the `floor` feature.

The key is to specify the special case for the floor:

1. `mid < sumCost.length - 1 && sumCost[mid] <= target && target < sumCost[mid + 1]`, found floor result at `sumCost[mid]`.
2. `mid > 0 && sumCost[mid - 1] <= target && target < sumCost[mid]`, found floor result at `sumCost[mid - 1]`.

The rest is normal binary search.

**Complexity:**

* **worst-case time complexity:** `O(log(n) * m)`, where `n` is the length of the input `cost`, `m` is the length of `val`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `cost`.
