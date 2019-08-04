# Lint486. Merge K Sorted Arrays

### LintCode

## Question

Given k sorted integer arrays, merge them into one sorted array.

**Example 1:**
```
Input: 
  [
    [1, 3, 5, 7],
    [2, 4, 6],
    [0, 8, 9, 10, 11]
  ]
Output: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```

**Example 2:**
```
Input:
  [
    [1,2,3],
    [1,2]
  ]
Output: [1,1,2,2,3]
```

**Challenge**

Do it in O(N log k).

**Note**

* N is the total number of integers.
* k is the number of arrays.

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param arrays: k sorted integer arrays
     * @return: a sorted array
     */
    public int[] mergekSortedArrays(int[][] arrays) {
        int[] res = new int[0];
        
        for (int[] arr : arrays) {
            res = merge(res, arr);
        }
        
        return res;
    }
    
    private int[] merge(int[] arr1, int[] arr2) {
        int n1 = arr1.length;
        int n2 = arr2.length;
        int[] res = new int[n1 + n2];
        for (int i = n1 + n2 - 1, j1 = n1 - 1, j2 = n2 - 1; i >= 0; i--) {
            int num1 = Integer.MIN_VALUE;
            int num2 = Integer.MIN_VALUE;
            if (j1 >= 0)
                num1 = arr1[j1];
            if (j2 >= 0) 
                num2 = arr2[j2];
            
            if (num1 > num2) {
                res[i] = num1;
                j1--;
            } else {
                res[i] = num2;
                j2--;
            }
        }
        return res;
    }
}
```

Merge K sorted arrays can be split to merge each array to the result array.

To merge to sorted array, we know the size (`n1 + n2`) of the result. Just need to compare the elements in the two sorted array and put them to the result.

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the length of the input `arrays`, `m` is the maximum length of the sorted arrays.
* **worst-case space complexity:** `O(n * m)`, where `n` is the length of the input `arrays`, `m` is the maximum length of the sorted arrays.

## Solution 2

* Java
```
public class Solution {
    /**
     * @param arrays: k sorted integer arrays
     * @return: a sorted array
     */
    public int[] mergekSortedArrays(int[][] arrays) {
        // write your code here
        int n = arrays.length;
        if (n == 0) 
            return new int[0];
        if (n == 1) 
            return arrays[0];
        if (n == 2) 
            return merge(arrays[0], arrays[1]);
        
        int mid = n / 2;
        return merge(mergekSortedArrays(Arrays.copyOfRange(arrays, 0, mid)),
                    mergekSortedArrays(Arrays.copyOfRange(arrays, mid, n)));
    }
    
    private int[] merge(int[] arr1, int[] arr2) {
        int n1 = arr1.length;
        int n2 = arr2.length;
        int[] res = new int[n1 + n2];
        for (int i = n1 + n2 - 1, j1 = n1 - 1, j2 = n2 - 1; i >= 0; i--) {
            int num1 = Integer.MIN_VALUE;
            int num2 = Integer.MIN_VALUE;
            if (j1 >= 0)
                num1 = arr1[j1];
            if (j2 >= 0) 
                num2 = arr2[j2];
            
            if (num1 > num2) {
                res[i] = num1;
                j1--;
            } else {
                res[i] = num2;
                j2--;
            }
        }
        return res;
    }
}
```

This question can be solved by `divided and conquer`. We can recursively divide the arrays into two shards until the size of the arrays is less than or equals to `2`. Then merge the sorted arrays.

**Complexity:**

* **worst-case time complexity:** `O(log(n) * m)`, where `n` is the length of the input `arrays`, `m` is the maximum length of the sorted arrays.
* **worst-case space complexity:** `O(n * m)`, where `n` is the length of the input `arrays`, `m` is the maximum length of the sorted arrays.
