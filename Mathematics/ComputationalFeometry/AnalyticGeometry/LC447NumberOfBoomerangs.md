# LC447. Number of Boomerangs

### LeetCode

## Question

Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points (i, j, k) such that the distance between i and j equals the distance between i and k (the order of the tuple matters).

Find the number of boomerangs. You may assume that n will be at most 500 and coordinates of points are all in the range [-10000, 10000] (inclusive).

**Example:**

**Input:**

```
[[0,0],[1,0],[2,0]]
```

**Output:**

```
2
```

**Explanation:**

The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]

## Solutions


* C++1 (1000ms)
```
int numberOfBoomerangs(vector<pair<int, int>>& points) {
    int booms = 0;
    for (auto &p : points) {
        unordered_map<double, int> ctr(points.size());
        for (auto &q : points)
            //hypot is the  square root of (x2+y2),distance
            booms += 2 * ctr[hypot(p.first - q.first, p.second - q.second)]++;
    }
    return booms;
}
```

* Java1 (282ms)
```
public class Solution {
    public int numberOfBoomerangs(int[][] points) {
        int res = 0;
        for(int i=0; i<points.length; ++i)
        {
            Map<Integer, Integer> groups = new HashMap<>();
            for(int j=0; j<points.length; ++j)
            {
                int dis = DistanceOf(points[i], points[j]);
                if(!groups.containsKey(dis)) groups.put(dis, 1);
                else groups.put(dis, groups.get(dis)+1);
            }
            for(Integer key : groups.keySet())
            {
                int size = groups.get(key);
                res += size *(size-1);
            }
        }
        return res;
    }
    private int DistanceOf(int[] point1, int[] point2)
    {
        int a = point1[0] - point2[0];
        int b = point1[1] - point2[1];
        return a*a + b*b;
    }
}
```

## Explanation

The Boomerangs needs at least two points with the same distance to a point. So the minimum number of points with the same distance to a point `X` is 3. We can add point with the same distance to a point `X` one by one, and see what happened:

```
number of points with the 
same distance to a point `X`: <2     2        3       4       5       6   ...
Boomerangs number :           0      1        3       6       10      15  ...
Added Boomerangs number  :    0      1        2       3       4       5   ...
```

Therefore, the number of Boomerangs of a point `X` is the sum of the `Added Boomerangs number`. So we can use the <a href="https://en.wikipedia.org/wiki/Triangular_number">Triangular Number</a>

![Triangular Number](Images/TriangularNumber.tiff)

Then, We just need to sum the Boomerangs number of all points.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n)