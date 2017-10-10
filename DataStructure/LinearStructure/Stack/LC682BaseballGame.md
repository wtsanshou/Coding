# LC682. Baseball Game

### LeetCode

## Question

You're now a baseball game point recorder.

Given a list of strings, each string can be one of the 4 following types:

1.  Integer (one round's score): Directly represents the number of points you get in this round.
2.  **+** (one round's score): Represents that the points you get in this round are the sum of the last two valid round's points.
3.  **D** (one round's score): Represents that the points you get in this round are the doubled data of the last valid round's points.
4.  **C** (an operation, which isn't a round's score): Represents the last valid round's points you get were invalid and should be removed.

Each round's operation is permanent and could have an impact on the round before and the round after.

You need to return the sum of the points you could get in all the rounds.

**Example 1:**
```
Input: ["5","2","C","D","+"]
Output: 30
```

**Explanation:** 
```
Round 1: You could get 5 points. The sum is: 5.
Round 2: You could get 2 points. The sum is: 7.
Operation 1: The round 2's data was invalid. The sum is: 5.  
Round 3: You could get 10 points (the round 2's data has been removed). The sum is: 15.
Round 4: You could get 5 + 10 = 15 points. The sum is: 30.
```

**Example 2:**
```
Input: ["5","-2","4","C","D","9","+","+"]
Output: 27
```

**Explanation:** 
```
Round 1: You could get 5 points. The sum is: 5.
Round 2: You could get -2 points. The sum is: 3.
Round 3: You could get 4 points. The sum is: 7.
Operation 1: The round 3's data is invalid. The sum is: 3.  
Round 4: You could get -4 points (the round 3's data has been removed). The sum is: -1.
Round 5: You could get 9 points. The sum is: 8.
Round 6: You could get -4 + 9 = 5 points. The sum is 13.
Round 7: You could get 9 + 5 = 14 points. The sum is 27.
```

**Note:**

* The size of the input list will be between 1 and 1000.
* Every integer represented in the list will be between -30000 and 30000.

## Solutions

* C++1
```
class Solution {
public:
    bool isNum(string num)
    {
        return isdigit(num[0]) || num[0]=='-';
    }
    
    int calPoints(vector<string>& ops) {
        int res=0, cur=0;
        vector<int> sta;
        for(string n : ops)
        {
            int s = sta.size();
            if(s==0 && !isNum(n)) continue;
            if(n == "C")
            {
                res -= sta.back();
                sta.pop_back();
            }
            else if(n == "+" && s > 1)
            {
                cur = sta[s-2] + sta[s-1];
                res += cur;
                sta.push_back(cur);
            }
            else if(n == "D")
            {
                cur = 2 * sta[s-1];
                res += cur;
                sta.push_back(cur);
            }
            else if(isNum(n))
            {
                cur = stoi(n);
                res += cur;
                sta.push_back(cur);
            }
        }
        return res;
    }
};
```

## Explanation

The ides is to use a stack to record all the integers. If found a operator, do the corresponding operation on the top number of the stack.

Corner cases:

1. Empty stack, but found a operator 
2. Only one integer in the stack, but found a operator '+'

**NOTE:** The limitation of the `Integer` is not clear. Integer with `+` is not considerd in the question

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)

