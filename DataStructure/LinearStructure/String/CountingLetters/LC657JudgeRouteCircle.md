# LC657. Judge Route Circle 

### LeetCode

## Question

 Initially, there is a Robot at position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to the original place.

The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are R (Right), L (Left), U (Up) and D (down). The output should be true or false representing whether the robot makes a circle.

**Example 1:**
```
Input: "UD"
Output: true
```

**Example 2:**
```
Input: "LL"
Output: false
```

## Solution

* C++1
```
bool judgeCircle(string moves) {
    vector<int> rlud(4);
    for(char m : moves){
        if(m=='R') rlud[0]++;
        else if(m=='L') rlud[1]++;
        else if(m=='U') rlud[2]++;
        else if(m=='D') rlud[3]++;
    }
    return rlud[0]==rlud[1] && rlud[2]==rlud[3];
}
```

## Explanation

Count the number of R (Right), L (Left), U (Up) and D (down). If the number of R (Right) and L (Left) are equal, and the number of U (Up) and D (down) are equal, the robot moves back to the original place.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1).
