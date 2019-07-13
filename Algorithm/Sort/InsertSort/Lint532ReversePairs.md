# Lint532. Reverse Pairs

Reverse pair is a pair of numbers (A[i], A[j]) such that A[i] > A[j] and i < j. Given an array, return the number of reverse pairs in the array.

**Example1**
```
Input:  A = [2, 4, 1, 3, 5]
Output: 3

Explanation:
(2, 1), (4, 1), (4, 3) are reverse pairs
```

**Example2**
```
Input:  A = [1, 2, 3, 4]
Output: 0

Explanation:
No reverse pair
```

## Solutions

### Solution 1

* Java
```
public long reversePairs(int[] A) {
    long res = 0;
    for(int j = 1; j < A.length; j++){
        int i=j;
        for(; i > 0; i--){
            if(A[i-1] > A[i]){
                int temp = A[i-1];
                A[i-1] = A[i];
                A[i] = temp;
            }
            else{
                break;
            }
        }
        res += j-i;
    }
    return res;
}
```

When I see question, the first idea is to have sorted list to store the elements before the index `j`, then I just need to find the index `i` where I can insert `A[j]` into it and keep the list sorted.

This is very similar with the <a href="WTInsertSort.md"> Insert Sort</a> algorithm.

**Note** We have to count the number of reverse pairs after find the index `i`.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the `A`.
* **worst-case space complexity:** O(1). 
