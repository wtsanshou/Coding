# LC419. Battleships in a Board

### LeetCode

## Question

Given an 2D board, count how many battleships are in it. The battleships are represented with 'X's, empty slots are represented with '.'s. You may assume the following rules:

* You receive a valid board, made of only battleships or empty slots.
* Battleships can only be placed horizontally or vertically. In other words, they can only be made of the shape 1xN (1 row, N columns) or Nx1 (N rows, 1 column), where N can be of any size.
* At least one horizontal or vertical cell separates between two battleships - there are no adjacent battleships.

**Example:**

```
X..X
...X
...X
In the above board there are 2 battleships.
```

**Invalid Example:**
```
...X
XXXX
...X
This is an invalid board that **you will not receive** - as battleships will always have a cell separating between them.
```

**Follow up:**

Could you do it in one-pass, using only O(1) extra memory and without modifying the value of the board?

## Solutions

### Solution 1

* C++ (6ms)
```
int countBattleships(vector<vector<char>>& board) {
    int row=board.size();
    int col = (row==0) ? 0 : board[0].size();
    int res=0;
    for(int i=0; i<row; ++i)
    {
        for(int j=0; j<col; ++j)
        {
            if(board[i][j]=='.') continue;
            if(i>0 && board[i-1][j]=='X') continue;
            if(j>0 && board[i][j-1]=='X') continue;
            res++;
        }
    }
    return res;
}
```

* Java (3ms)
```
public int countBattleships(char[][] board) {
    int row = board.length;
    int col = (row>0) ? board[0].length : 0;
    int res =0;
    for(int i=0; i<row; ++i)
    {
        for(int j=0; j<col; ++j)
        {
            if(board[i][j] == '.') continue;
            if(i>0 && board[i-1][j] == 'X') continue;
            if(j>0 && board[i][j-1] == 'X') continue;
            res++;
        }
    }
    return res;
}
```

Note **you will not receive** - as battleships will always have a cell separating between them.

So, we just need to count the number of the head of each battleship.

**Complexity:**

* **worst-case time complexity:** `O(h * w)`, where `h` is the height of the input `board`, `w` is the width of the `board`.
* **worst-case space complexity:** `O(1)`.
