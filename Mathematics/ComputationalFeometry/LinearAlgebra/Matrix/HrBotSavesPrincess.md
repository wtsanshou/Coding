# Hr. Bot Baves Princess

### HackerRank

## Question

Princess Peach is trapped in one of the four corners of a square grid. You are in the center of the grid and can move one step at a time in any of the four directions. Can you rescue the princess?

**Input format**

The first line contains an odd integer N (3 <= N < 100) denoting the size of the grid. This is followed by an NxN grid. Each cell is denoted by '-' (ascii value: 45). The bot position is denoted by 'm' and the princess position is denoted by 'p'.

Grid is indexed using Matrix Convention

**Output format**

Print out the moves you will take to rescue the princess in one go. The moves must be separated by '\n', a newline. The valid moves are LEFT or RIGHT or UP or DOWN.

**Sample input**
```
3
---
-m-
p--
```

**Sample output**
```
DOWN
LEFT
```

**Task**

Complete the function displayPathtoPrincess which takes in two parameters - the integer N and the character array grid. The grid will be formatted exactly as you see it in the input, so for the sample input the princess is at grid[2][0]. The function shall output moves (LEFT, RIGHT, UP or DOWN) on consecutive lines to rescue/reach the princess. The goal is to reach the princess in as few moves as possible.

The above sample input is just to help you understand the format. The princess ('p') can be in any one of the four corners.

**Scoring**

Your score is calculated as follows : (NxN - number of moves made to rescue the princess)/10, where N is the size of the grid (3x3 in the sample testcase).

## Solutions

* Java1
```
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int si=0, sj=0, ei=0, ej=0;
        for(int i=0; i<N; ++i){
            String line = sc.next();
            char[] c = line.toCharArray();
            for(int j=0; j<N; ++j){
                if(c[j] == 'm'){
                    si = i;
                    sj = j;
                }
                else if(c[j] == 'p'){
                    ei = i;
                    ej = j;
                }
            }                
        }
        while(si!=ei || sj!=ej){
            if(si<ei){
                si++;
                System.out.println("DOWN");
            }
            else if(si>ei){
                si--;
                System.out.println("UP");
            }
            
            if(sj < ej){
                sj++;
                System.out.println("RIGHT");
            }
            else if(sj > ej){
                sj--;
                System.out.println("LEFT");
            }
        }
    }
```

## Explanation

1. Find the coordinates of me and princess.
2. Move from my location to princess's location.

* **worst-case time complexity:** O(N<sup>2</sup>)
* **worst-case space complexity:** O(N)

