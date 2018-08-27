# LC888. Fair Candy Swap

### LeetCode

## Question

Alice and Bob have candy bars of different sizes: A[i] is the size of the i-th bar of candy that Alice has, and B[j] is the size of the j-th bar of candy that Bob has.

Since they are friends, they would like to exchange one candy bar each so that after the exchange, they both have the same total amount of candy.  (The total amount of candy a person has is the sum of the sizes of candy bars they have.)

Return an integer array ans where ans[0] is the size of the candy bar that Alice must exchange, and ans[1] is the size of the candy bar that Bob must exchange.

If there are multiple answers, you may return any one of them.  It is guaranteed an answer exists.

**Example 1:**
```
Input: A = [1,1], B = [2,2]
Output: [1,2]
```

**Example 2:**
```
Input: A = [1,2], B = [2,3]
Output: [1,2]
```

**Example 3:**
```
Input: A = [2], B = [1,3]
Output: [2,3]
```

**Example 4:**
```
Input: A = [1,2,5], B = [2,4]
Output: [5,4]
```

**Note:**

* 1 <= A.length <= 10000
* 1 <= B.length <= 10000
* 1 <= A[i] <= 100000
* 1 <= B[i] <= 100000
* It is guaranteed that Alice and Bob have different total amounts of candy.
* It is guaranteed there exists an answer.

## Solutions

* Scala1 O(n<sup>2</sup>)
```
def fairCandySwap(A: Array[Int], B: Array[Int]): Array[Int] = {
    val distance = (A.sum - B.sum)/2
    val first= A.find(a => B.contains(a-distance)).head
    Array(first, first-distance)
}
```

* Scala2 O(n)
```
def fairCandySwap(A: Array[Int], B: Array[Int]): Array[Int] = {
    val distance = (A.sum - B.sum)/2
    val setA = A.toSet
    val setB = B.toSet
    val first= setA.find(a => setB.contains(a-distance)).head
    Array(first, first-distance)
}
```

## Explanation

The different between the two exchanged numbers are the half of the different between the sums of the two arrays.

* **worst-case time complexity:** O(max(n, m)), where `n` is the length of the array `A`,  `m` is the length of the array `B`.
* **worst-case space complexity:** O(1)
