# WT. Select Sort

## Implement Select Sort

**Example 1:**
```
    Input:  [3, 2, 1, 4, 5]
    Output: [1, 2, 3, 4, 5]
```

**Example 2:**
```
    Input:  [1, 1, 2, 1, 1]
    Output: [1, 1, 1, 1, 2]
``` 

## Solution

* Java
```
public void sortIntegers(int[] A) {
    for(int j=0; j<A.length-1; j++){
        int k=j;
        int min = A[k];
        for(int i=j; i<A.length; i++){
            if(A[i] < min){
                min = A[i];
                k = i;
            }
        }
        int temp = A[j];
        A[j] = A[k];
        A[k] = temp;
    }
}
```

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the `A`.
* **worst-case space complexity:** O(1).