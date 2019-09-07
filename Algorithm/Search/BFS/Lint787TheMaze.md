# Lint787. The Maze

### LintCode (Medium)

## Question

There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the ball's start position, the destination and the maze, determine whether the ball could stop at the destination.

The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The start and destination coordinates are represented by row and column indexes.

**Example 1:**
```
Input:
map = 
[
 [0,0,1,0,0],
 [0,0,0,0,0],
 [0,0,0,1,0],
 [1,1,0,1,1],
 [0,0,0,0,0]
]
start = [0,4]
end = [3,2]

Output:
false
```

**Example 2:**
```
Input:
map = 
[[0,0,1,0,0],
 [0,0,0,0,0],
 [0,0,0,1,0],
 [1,1,0,1,1],
 [0,0,0,0,0]
]
start = [0,4]
end = [4,4]

Output:
true
```

**Notice**

1. There is only one ball and one destination in the maze.
2. Both the ball and the destination exist on an empty space, and they will not be at the same position initially.
3. The given maze does not contain border (like the red rectangle in the example pictures), but you could assume the border of the maze are all walls.
4. The maze contains at least 2 empty spaces, and both the width and height of the maze won't exceed 100.

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param maze: the maze
     * @param start: the start
     * @param destination: the destination
     * @return: whether the ball could stop at the destination
     */
    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        int h = maze.length;
        int w = maze[0].length;
        
        boolean[][] visited = new boolean[h][w];
        Queue<Integer> queue = new LinkedList<>();
        
        queue.offer(start[0] * w + start[1]);
        visited[start[0]][start[1]] = true;
        
        int[] dirs = {1, 0, -1, 0, 1};
        
        while (!queue.isEmpty()) {
            int cur = queue.poll();
            
            for (int i = 0; i < 4; i++) {
                int x = cur / w;
                int y = cur % w;
                while (isNotWall(maze, x, y)) {
                    x += dirs[i];
                    y += dirs[i + 1];
                }
                
                x -= dirs[i]; // move back from wall
                y -= dirs[i + 1]; // move back from wall
                
                if (isDesitination(destination, x, y)) {
                    return true;
                }
                
                if (!visited[x][y]) {
                    queue.offer(x * w + y);
                    visited[x][y] = true;
                }
            }
        }
        
        return false;
    }
    
    private boolean isNotWall(int[][] maze, int x, int y) {
        return x >= 0 && x < maze.length && y >= 0 && y < maze[0].length && maze[x][y] != 1;
    }
    
    private boolean isDesitination(int[] destination, int x, int y) {
        return destination[0] == x && destination[1] == y;
    }
}
```

It's a BFS solving maze problem. The different here is that `it won't stop rolling until hitting a wall` instead of one step each time. So we can use a while loop to find the next move.

Here I learned a way to use `1D` array `int[] dirs = {1, 0, -1, 0, 1}` to represent 4 directions. 

I also learned a way to use one integer (`i * w + j`) to represent 2D index `(i, j)`.

**Complexity:**

* **worst-case time complexity:** `O(h * w)`, where `h` is height of the `maze`, `w` is the width of the `maze`.
* **worst-case space complexity:** `O(h * w)`, where `h` is height of the `maze`, `w` is the width of the `maze`.
