# LC922. Sort Array By Parity II

### LeetCode

## Question

Given an array A of non-negative integers, half of the integers in A are odd, and half of the integers are even.

Sort the array so that whenever A[i] is odd, i is odd; and whenever A[i] is even, i is even.

You may return any answer array that satisfies this condition.

**Example 1:**
```
Input: [4,2,5,7]
Output: [4,5,2,7]
Explanation: [4,7,2,5], [2,5,4,7], [2,7,4,5] would also have been accepted.
```

**Note:**

* 2 <= A.length <= 20000
* A.length % 2 == 0
* 0 <= A[i] <= 1000

## Solutions

* Scala1
```
def sortArrayByParityII(A: Array[Int]): Array[Int] = {
    val (a, b) = A.partition(_%2==0)
    a.zip(b).map(x => Array(x._1, x._2)).flatten
}
```

## Explanation

1. Separate the even and odd.
2. Zip each pair.
3. Convert to array and flatten.

* **worst-case time complexity:** `O(N)`, where `N` is the length of the `A`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the `A`.
