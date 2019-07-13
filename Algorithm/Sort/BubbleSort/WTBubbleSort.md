# WT. Bubble Sort

## Question

Implement `Bubble Sort`

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
    for(int j=A.length-1; j>0; j--){
        for(int i=0; i<j; i++){
            if(A[i] > A[i+1]){
                int temp = A[i];
                A[i] = A[i+1];
                A[i+1] = temp;
            }
        }
    }
}
```

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the `A`.
* **worst-case space complexity:** O(1).

