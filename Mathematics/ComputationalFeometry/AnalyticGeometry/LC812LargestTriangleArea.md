# LC812. Largest Triangle Area

### LeetCode

## Questions

You have a list of points in the plane. Return the area of the largest triangle that can be formed by any 3 of the points.

**Example:**
```
Input: points = [[0,0],[0,1],[1,0],[0,2],[2,0]]
Output: 2
Explanation: 
The five points are show in the figure below. The red triangle is the largest.
```

![LC812. Largest Triangle Area](Images/LC812LargestTriangleArea.png)

**Notes:**

* 3 <= points.length <= 50.
* No points will be duplicated.
* -50 <= points[i][j] <= 50.
* Answers within 10^-6 of the true value will be accepted as correct.

## Solutions

* Scala1
```
object Solution {

  def largestTriangleArea(points: Array[Array[Int]]): Double = {
    val triangles = for{
      a <- points
      b <- points
      c <- points
    } yield getArea(a, b, c)

    triangles.max
  }
    
  def getArea(a: Array[Int], b: Array[Int], c: Array[Int]): Double = {
    Math.abs(a(0) * (b(1) - c(1)) + b(0) * (c(1) - a(1)) + c(0) * (a(1) - b(1))).toDouble / 2.0
  }
    
}
```

## Explanation

Calculate the areas of all trangles, find the Largest Triangle Area.

* **worst-case time complexity:** O(N<sup>3</sup>), where `N` is the points of the map.
* **worst-case space complexity:** O(N<sup>3</sup>), where `N` is the points of the map.
