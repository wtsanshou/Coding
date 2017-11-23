# LC390. Elimination Game

### LeetCode

## Question

There is a list of sorted integers from 1 to n. Starting from left to right, remove the first number and every other number afterward until you reach the end of the list.

Repeat the previous step again, but this time from right to left, remove the right most number and every other number from the remaining numbers.

We keep repeating the steps again, alternating left to right and right to left, until a single number remains.

Find the last number that remains starting with a list of length n.

**Example:**

**Input:**

```
n = 9,
1 2 3 4 5 6 7 8 9
2 4 6 8
2 6
6
```

**Output:**

```
6
```

## Solutions

* C++1
```
int lastRemaining(int n) {
    if(n<1) return 0;
    int start = 1, step = 1, remaining = n;
    bool leftToRight = true;
    while(remaining > 1)
    {
        if(leftToRight || remaining%2 == 1)
            start += step;
        remaining /= 2;
        step *= 2;
        leftToRight = !leftToRight;
    }
    return start;
}
```

* C++2
```
int lastRemaining(int n) {
    return (n==1)? 1 : 2*(1 + n/2 - lastRemaining(n/2));
}
```

## Explanation

The last number of remaining must be the first and the only number of the remaining number.

So, the solution is to track the first number of the remaining numbers after removing. 

For odd remaining numbers, we will remove `(remaining+1)/2` numbers; for even remaining number, we will remove `remaining/2` numbers.

Only remove from left to right or the remaining numbers are odd, the old first number will be removed. Because each time removing half of the remaining numbers, the moving step will exponential increase.

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)
