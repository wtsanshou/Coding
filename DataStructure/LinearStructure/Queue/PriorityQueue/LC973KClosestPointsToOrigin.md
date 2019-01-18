# LC973. K Closest Points to Origin

### LeetCode

## Question

We have a list of points on the plane.  Find the K closest points to the origin (0, 0).

(Here, the distance between two points on a plane is the Euclidean distance.)

You may return the answer in any order.  The answer is guaranteed to be unique (except for the order that it is in.)

**Example 1:**
```
Input: points = [[1,3],[-2,2]], K = 1
Output: [[-2,2]]
Explanation: 
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest K = 1 points from the origin, so the answer is just [[-2,2]].
```

**Example 2:**
```
Input: points = [[3,3],[5,-1],[-2,4]], K = 2
Output: [[3,3],[-2,4]]
(The answer [[-2,4],[3,3]] would also be accepted.)
```

**Note:**

* 1 <= K <= points.length <= 10000
* -10000 < points[i][0] < 10000
* -10000 < points[i][1] < 10000

## Solutions
* Scala1
```
def kClosest(points: Array[Array[Int]], K: Int): Array[Array[Int]] = {
    val order = Ordering.by { p: Array[Int] => Math.sqrt(p(0) * p(0) + p(1) * p(1)) }
    val priorityQ = new scala.collection.mutable.PriorityQueue[Array[Int]]()(order)
    points.foreach(p => {
        priorityQ.enqueue(p)
        if(priorityQ.size > K) priorityQ.dequeue()
    })
    priorityQ.toArray
}
```

## Explanation

Using a priority queue to store the most closest `K` points. 

* **worst-case time complexity:** `O(N)`, where `N` is the number of the `points`.
* **worst-case space complexity:** `O(N)`, where `N` is the number of the `points`.
