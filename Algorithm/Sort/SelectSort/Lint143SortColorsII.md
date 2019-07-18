# Lint143. Sort Colors II

### LintCode

## Question

Given an array of n objects with k different colors (numbered from 1 to k), sort them so that objects of the same color are adjacent, with the colors in the order 1, 2, ... k.

**Example 1**
```
Input: 
[3,2,2,1,4] 
4

Output: 
[1,2,2,3,4]
```

**Example 2**
```
Input: 
[2,1,1,2,2] 
2

Output: 
[1,1,2,2,2]
```

**Challenge**

A rather straight forward solution is a two-pass algorithm using counting sort. That will cost O(k) extra memory. Can you do it without using extra memory?

**Notice**

You are not suppose to use the library's sort function for this problem.
k <= n

## Solutions

### Solution 1

* Java
```
public void sortColors2(int[] colors, int k) {
    for (int i = 0, key = 1; key <= k; key++) {
        for (int j = i; j < colors.length; j++) {
            if (colors[j] == key) {
                colors[j] = colors[i];
                colors[i++] = key;
            }
        }
    }
}
```

The faster solution should be the cost O(k) extra memory solution. The second one should be quick sort. But both of them need extra memory.

If extra memory is not allowed, we can select to use `bubble`, `insert`, or `select` sort. I think `select sort` is most suitable for this question.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of `colors`.
* **worst-case space complexity:** `O(1)`.
