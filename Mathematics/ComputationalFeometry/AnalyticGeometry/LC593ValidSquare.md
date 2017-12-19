# LC593. Valid Square

### LeetCode

## Question

Given the coordinates of four points in 2D space, return whether the four points could construct a square.

The coordinate (x,y) of a point is represented by an integer array with two integers.

**Example:**

**Input:** 

```
p1 = [0,0], p2 = [1,1], p3 = [1,0], p4 = [0,1]
```

**Output:** 

```
True
```

**Note:**

* All the input integers are in the range [-10000, 10000].
* A valid square has four equal sides with positive length and four equal angles (90-degree angles).
* Input points have no order.

## Solutions

* C++1 (could solve range more than 10000)
```
class Solution {
public:
    double lenFrom(vector<int>& p1, vector<int>& p2)
    {
        double a = p1[0] - p2[0];
        double b = p1[1] - p2[1];
        return a*a + b*b;
    }
    bool validSquare(vector<int>& p1, vector<int>& p2, vector<int>& p3, vector<int>& p4) {
        vector<double> lens(6);
        lens[0] = lenFrom(p1, p2);
        lens[1] = lenFrom(p1, p3);
        lens[2] = lenFrom(p1, p4);
        lens[3] = lenFrom(p2, p3);
        lens[4] = lenFrom(p2, p4);
        lens[5] = lenFrom(p3, p4);
        sort(lens.begin(), lens.end());
        for(int i=0; i<3; ++i)
            if(abs(lens[i]-lens[i+1]) > 1e-9)
                return false;
        if(abs(lens[4]-lens[5]) > 1e-9) return false;
        if(abs(lens[0]-lens[5]) < 1e-9) return false;
        if(abs(lens[0]-lens[5]/2) > 1e-9) return false;
        return true;
    }
};
```

* C++2
```
class Solution {
public:
    int d(vector<int>& p1, vector<int>& p2) {
        return (p1[0] - p2[0]) * (p1[0] - p2[0]) + (p1[1] - p2[1]) * (p1[1] - p2[1]);
    }
    bool validSquare(vector<int>& p1, vector<int>& p2, vector<int>& p3, vector<int>& p4) {
        unordered_set<int> s({ d(p1, p2), d(p1, p3), d(p1, p4), d(p2, p3), d(p2, p4), d(p3, p4) });
        return !s.count(0) && s.size() == 2;
    }
};
```

## Explanation

For a square, the four edges should be equals, the diagonals should be equals. The edge should not equals the diagonal.

So Only two lengths between each two points, and no any two points are on the same location.

**Corner cases:**

1. The four points are at the same location.
