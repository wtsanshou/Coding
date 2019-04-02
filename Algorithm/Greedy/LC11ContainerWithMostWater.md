# LC11. Container With Most Water

### LeetCode

## Question

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and n is at least 2.

## Solutions
 
### Solution 1

* C++
```
int maxArea(vector<int>& height) {
    int i=0, j=height.size()-1;
    int res = 0;
    while(i<j)
    {
        int minH = min(height[i], height[j]);
        res = max(res, (j-i)*minH);
        while(height[i]<=minH && i<j) i++;
        while(height[j]<=minH && i<j) j--;
    }
    return res;
}
```

There are two factors (width and height) which can affect the capacity of the container.

We can search from the most left and right to the middle which means from most wide to narrow. Only higher height can compensate the lost of narrow width.

**Note:** the lower height decides the capacity of the container. 

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `height`.
* **worst-case space complexity:** `O(1)`