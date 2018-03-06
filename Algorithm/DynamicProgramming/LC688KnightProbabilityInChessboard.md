# LC688. Knight Probability in Chessboard

### LeetCode

## Question

On an `NxN` chessboard, a knight starts at the r<sup>th</sup> row and c<sup>th</sup> column and attempts to make exactly `K` moves. The rows and columns are 0 indexed, so the top-left square is `(0, 0)`, and the bottom-right square is `(N-1, N-1)`.

A chess knight has `8` possible moves it can make, as illustrated below. Each move is two squares in a cardinal direction, then one square in an orthogonal direction.


Each time the knight is to move, it chooses one of eight possible moves uniformly at random (even if the piece would go off the chessboard) and moves there.

The knight continues moving until it has made exactly K moves or has moved off the chessboard. Return the probability that the knight remains on the board after it has stopped moving.

**Example:**

```
Input: 3, 2, 0, 0
Output: 0.0625
Explanation: There are two moves (to (1,2), (2,1)) that will keep the knight on the board.
From each of those positions, there are also two moves that will keep the knight on the board.
The total probability the knight stays on the board is 0.0625.
```

**Note:**

* N will be between 1 and 25.
* K will be between 0 and 100.
* The knight always initially starts on the board.

## Solutions

* Java1 (TLE)
```
class Solution {
    
    private int[] steps = {-2, -1, 1, 2};
    private int stepSize = 4;
    
    public double knightProbability(int N, int K, int r, int c) {
        if(K == 0) return 1;
        double result = 0.0;
        for(int i=0; i<stepSize; ++i){
            for(int j=0; j<stepSize; ++j){
                if(Math.abs(steps[i]) != Math.abs(steps[j]) && isInBoard(N, r+steps[i], c+steps[j])){
                    result += 0.125 * knightProbability(N, K-1, r+steps[i], c+steps[j]);
                }
            }
        }
        return result;
    }
    
    private boolean isInBoard(int N, int r, int c){
        return r>=0 && r<N && c>=0 && c<N;
    }
}
```

* Java2
```
class Solution {
    
    private int[] steps = {-2, -1, 1, 2};
    private int stepSize = 4;
    
    public double knightProbability(int N, int K, int r, int c) {
        double[][] dp = new double[N][N];
        dp[r][c] = 1;
        
        dp = addKLayersProbability(N, K, dp);
      
        return sumProbability(dp);
    }
    
    private double[][] addKLayersProbability(int N, int K, double[][] dp){
        for (int i=0; i< K; ++i) {
            dp = addALayerProbability(dp, N);
        }
        return dp;
    }
    
    private double[][] addALayerProbability(double[][] dp, int N){
        double[][] dp2 = new double[N][N];
        for (int row = 0; row < N; row++) {
            for (int col = 0; col < N; col++) {
                put8PossibleMoves(dp, dp2, N, row, col);
            }
        }
        return dp2;
    }
    
    private void put8PossibleMoves(double[][] dp, double[][] dp2, int N,  int row, int col){
        for(int i=0; i<stepSize; ++i){
            for(int j=0; j<stepSize; ++j){
                if(canJumpTo(i, j) && isInBoard(N, row+steps[i], col+steps[j])){
                    dp2[row+steps[i]][col+steps[j]] += dp[row][col] / 8.0;
                }
            }
        }
    }
    
    private boolean canJumpTo(int i, int j){
        return Math.abs(steps[i]) != Math.abs(steps[j]);
    }
    
    private boolean isInBoard(int N, int r, int c){
        return r>=0 && r<N && c>=0 && c<N;
    }
    
    private double sumProbability(double[][] dp){
        double result = 0.0;
        for(double[] row : dp){
            for(double ele : row)
                result += ele;
        }
        return result;
    }
}
```

## Explanation

Adding `K` layers' probability. Using Dynamic programming to remember each layer's probability.

Because at the beginning, except `dp[r][c]`, all vlues of the `dp`  are `0`. So each layer, we just calculate the place where the knight stays on the board.

* **worst-case time complexity:** O(N<sup>2</sup>K), where `N` is the width/height of the chessboard, `K` is the number of steps.
* **worst-case space complexity:** O(N<sup>2</sup>), where `N` is the width/height of the chessboard
