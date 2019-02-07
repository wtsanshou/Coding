# LC986. Interval List Intersections

### LeetCode

## Question

Given two lists of closed intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

(Formally, a closed interval [a, b] (with a <= b) denotes the set of real numbers x with a <= x <= b.  The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval.  For example, the intersection of [1, 3] and [2, 4] is [2, 3].)

**Example 1:**
```
Input: A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
Reminder: The inputs and the desired output are lists of Interval objects, and not arrays or lists.
``` 

**Note:**

* 0 <= A.length < 1000
* 0 <= B.length < 1000
* 0 <= A[i].start, A[i].end, B[i].start, B[i].end < 10^9

## Solutions

* Scala1
```
def intervalIntersection(A: Array[Interval], B: Array[Interval]): Array[Interval] = {
    var result = Array[Interval]()
    val AB = A ++: B
    if(AB.isEmpty) return result
    val sortedAB = AB.sortBy(ab => ab.start)
    var temp = sortedAB(0)
    for(i <- 1 until sortedAB.size){
        if(sortedAB(i).start <= temp.end)
            result = result :+ new Interval(sortedAB(i).start, Math.min(sortedAB(i).end,temp.end))
        temp = new Interval(sortedAB(i).start, Math.max(sortedAB(i).end, temp.end))
    }
    result
}
```

## Explanation

It's a typical greedy algorithm.

The `sortedAB` could be improved, because `A` and `B` are all sorted by their `start`. We can use `O(n)` to get the `sortedAB`.

* **worst-case time complexity:** `O(n*log(n))`, where `n` is the length of array `A` and the length of array `B`.
* **worst-case space complexity:** `O(n*log(n))`, where `n` is the length of array `A` and the length of array `B`.
