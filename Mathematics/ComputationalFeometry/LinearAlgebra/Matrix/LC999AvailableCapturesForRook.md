# LC999. Available Captures for Rook

### LeetCode

## Question

On an 8 x 8 chessboard, there is one white rook.  There also may be empty squares, white bishops, and black pawns.  These are given as characters 'R', '.', 'B', and 'p' respectively. Uppercase characters represent white pieces, and lowercase characters represent black pieces.

The rook moves as in the rules of Chess: it chooses one of four cardinal directions (north, east, west, and south), then moves in that direction until it chooses to stop, reaches the edge of the board, or captures an opposite colored pawn by moving to the same square it occupies.  Also, rooks cannot move into the same square as other friendly bishops.

Return the number of pawns the rook can capture in one move.
 
**Example 1:**

![LC999. Available Captures for Rook](Images/LC999AvailableCapturesForRook1.png)
```
Input: [[".",".",".",".",".",".",".","."],[".",".",".","p",".",".",".","."],[".",".",".","R",".",".",".","p"],[".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".","."],[".",".",".","p",".",".",".","."],[".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".","."]]
Output: 3
Explanation: 
In this example the rook is able to capture all the pawns.
```

**Example 2:**

![LC999. Available Captures for Rook](Images/LC999AvailableCapturesForRook2.png)
```
Input: [[".",".",".",".",".",".",".","."],[".","p","p","p","p","p",".","."],[".","p","p","B","p","p",".","."],[".","p","B","R","B","p",".","."],[".","p","p","B","p","p",".","."],[".","p","p","p","p","p",".","."],[".",".",".",".",".",".",".","."],[".",".",".",".",".",".",".","."]]
Output: 0
Explanation: 
Bishops are blocking the rook to capture any pawn.
```

**Example 3:**

![LC999. Available Captures for Rook](Images/LC999AvailableCapturesForRook3.png)
```
Input: [[".",".",".",".",".",".",".","."],[".",".",".","p",".",".",".","."],[".",".",".","p",".",".",".","."],["p","p",".","R",".","p","B","."],[".",".",".",".",".",".",".","."],[".",".",".","B",".",".",".","."],[".",".",".","p",".",".",".","."],[".",".",".",".",".",".",".","."]]
Output: 3
Explanation: 
The rook can capture the pawns at positions b5, d6 and f5.
``` 

**Note:**

* board.length == board[i].length == 8
* board[i][j] is either 'R', '.', 'B', or 'p'
* There is exactly one cell with board[i][j] == 'R'

## Solutions

### Solution 1

* Java
```
class Solution {
    public int numRookCaptures(char[][] board) {
        int[] R = findRook(board);
        int pawns = 0;
        for(int i=R[0]; i>=0; i--){
            if(board[i][R[1]] == 'B') break;
            else if(board[i][R[1]] == 'p'){
                pawns++;
                break;
            }
        }
        for(int i=R[0]; i<board.length; i++){
            if(board[i][R[1]] == 'B') break;
            else if(board[i][R[1]] == 'p'){
                pawns++;
                break;
            }
        }
        for(int i=R[1]; i>=0; i--){
            if(board[R[0]][i] == 'B') break;
            else if(board[R[0]][i] == 'p'){
                pawns++;
                break;
            }
        }
        for(int i=R[1]; i<board.length; i++){
            if(board[R[0]][i] == 'B') break;
            else if(board[R[0]][i] == 'p'){
                pawns++;
                break;
            }
        }
        return pawns;
    }
    
    private int[] findRook(char[][] board){
        for(int i=0; i<board.length; i++)
            for(int j=0; j<board[0].length; j++)
                if(board[i][j] == 'R')
                    return new int[]{i,j};
        return new int[2];
    }
}
```

The code looks too long. I have not got a solution to clean it up.

* **worst-case time complexity:** `O(m * n)`, where `m` is the row of the `board`, n is the height of the `board`.
* **worst-case space complexity:** `O(1)`
