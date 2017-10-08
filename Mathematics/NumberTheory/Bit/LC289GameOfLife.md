# LC289. Game of Life

### LeetCode

## Question

According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

1. Any live cell with fewer than two live neighbors dies, as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population..
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

Write a function to compute the next state (after one update) of the board given its current state.

**Follow up:** 

1. Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
2. In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

## Solutions

* C++1
```
void gameOfLife(vector<vector<int>>& board) {
        int h = board.size();
        int w = (h>0) ? board[0].size() : 0;
        for(int i=0; i<h; ++i)
        {
            for(int j=0; j<w; ++j)
            {
                int lives = 0;
                for(int x=((i<1)? 0 :i-1); x<=((i+1)<h ? i+1 : h-1); ++x)
                    for(int y=((j<1)? 0 :j-1); y<=((j+1)<w ? j+1 : w-1); ++y)
                        lives += board[x][y] & 1;
                if(lives==3 || (lives==4 && board[i][j]==1))
                    board[i][j] |= 2;
            }
        }
        for(int i=0; i<h; ++i)
            for(int j=0; j<w; ++j)
                board[i][j] >>= 1;
}
```

* C++2
```
class Solution {
public:
    int lifeInNineCells(vector<vector<int>>& board, int m, int n, int row, int col)
    {
        int count=0;
        for(int i=max(row-1, 0); i<min(row+2,m); ++i)
        {
            for(int j=max(col-1, 0); j<min(col+2, n); ++j)
                count += board[i][j]&1;
        }
        return count;
    }
    void gameOfLife(vector<vector<int>>& board) {
        int m=board.size(), n= m? board[0].size() : 0;
        for(int i=0; i<m; ++i)
        {
            for(int j=0; j<n; ++j)
            {
                int lives = lifeInNineCells(board, m, n, i, j);
                if(lives==3 || lives-board[i][j]==3)
                    board[i][j] |= 2;
            }
        }
        for(int i=0; i<m; ++i)
        {
            for(int j=0; j<n; ++j)
            {
                board[i][j] >>= 1;
            }
        }
    }
};
```

## Explanation

The most straight forward way is using an 2D array to record the next state (after one update) of the board. The worst-case space complexity is O(n<sup>2</sup>)

Because there are just two states (live (1) or dead (0)), we can use another bit to record the next state (after one update) of the board. The updated state will not affect the initial state.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(1)
