# LC905. Sort Array By Parity

### LeetCode

## Question

Given an array A of non-negative integers, return an array consisting of all the even elements of A, followed by all the odd elements of A.

You may return any answer array that satisfies this condition.

**Example 1:**
```
Input: [3,1,2,4]
Output: [2,4,3,1]
The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.
``` 

**Note:**

* 1 <= A.length <= 5000
* 0 <= A[i] <= 5000

## Solutions

* Scala1
```
def sortArrayByParity(A: Array[Int]): Array[Int] = {
    A.filter(_%2==0) ++: A.filter(_%2!=0)
}
```

* Scala2
```
def sortArrayByParity(A: Array[Int]): Array[Int] = {
    A.filter(_%2==0) ++ A.filter(_%2!=0)
}
```

* Scala3
```
def sortArrayByParity(A: Array[Int]): Array[Int] = {
    val (evens, odds) = A.partition(_ % 2 == 0)
    evens ++ odds
}
```

## Explanation

Using two pointers `i` and `j`, `j` is to traverse the array, move `i` only when the element does not equal `val`.

* **worst-case time complexity:** `O(N)`, where `N` is the length of the `A`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the `A`.

