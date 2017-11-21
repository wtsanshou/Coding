# LC130. Surrounded Regions

### LeetCode

## Question

Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

For example,

```
X X X X
X O O X
X X O X
X O X X
```

After running your function, the board should be:

```
X X X X
X X X X
X X X X
X O X X
```

## Solutions

* C++1
```
void DFS(vector<vector<char>>& board, int i, int j)
    {
        board[i][j] = 'S';
        if(i-1>0 && board[i-1][j] == 'O') DFS(board, i-1, j);
        if(i+1<board.size() && board[i+1][j] == 'O') DFS(board, i+1, j);
        if(j-1>0 && board[i][j-1] == 'O') DFS(board, i, j-1);
        if(j+1<board[0].size() && board[i][j+1] == 'O') DFS(board, i, j+1);
    }
    void solve(vector<vector<char>>& board) {
        int h = board.size();
        int w = h>0 ? board[0].size() : 0;
        for(int i=0; i<h; ++i)
        {
            if(board[i][0] == 'O') DFS(board, i, 0);
            if(board[i][w-1] == 'O') DFS(board, i, w-1);
        }
        for(int i=1; i<w-1; ++i)
        {
            if(board[0][i] == 'O') DFS(board, 0, i);
            if(board[h-1][i] == 'O') DFS(board, h-1, i);
        }
        for(int i=0; i<h; ++i)
            for(int j=0; j<w; ++j)
                if(board[i][j] == 'S') board[i][j] = 'O';
                else board[i][j] = 'X';
    }
```

## Explanation

Only the 'O's connect to any edge of the board will not be surrounded.

Using DFS to mark any 'O's connect to any edge of the board.

* **worst-case time complexity:** O(h * w)
* **worst-case space complexity:** O(h * w)

