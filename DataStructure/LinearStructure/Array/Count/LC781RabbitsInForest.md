# LC781. Rabbits in Forest

### LeetCode

## Question

In a forest, each rabbit has some color. Some subset of rabbits (possibly all of them) tell you how many other rabbits have the same color as them. Those answers are placed in an array.

Return the minimum number of rabbits that could be in the forest.

**Examples 1:**
```
Input: answers = [1, 1, 2]
Output: 5
```

**Explanation:**

The two rabbits that answered "1" could both be the same color, say red.

The rabbit than answered "2" can't be red or the answers would be inconsistent.

Say the rabbit that answered "2" was blue.

Then there should be 2 other blue rabbits in the forest that didn't answer into the array.

The smallest possible number of rabbits in the forest is therefore 5: 3 that answered plus 2 that didn't.

**Examples 2:**
```
Input: answers = [10, 10, 10]
Output: 11
```

**Examples 3:**
```
Input: answers = []
Output: 0
```

**Note:**

* answers will have length at most 1000.
* Each answers[i] will be an integer in the range [0, 999].

## Solutions

* Java1
```
public int numRabbits(int[] answers) {
    int[] count = new int[1000];
    int res = 0;
    for(int answer : answers)
        count[answer]++;
    for(int i=0; i<1000; ++i)
        if(count[i] != 0)
            res += ((count[i] + i)/(i+1))*(i+1);
    return res;
}
```

## Explanation

Based on the question, we can see the same color rabbits will tell the same number. 

To minimum the number of the rabbits, we can try to put possible maximum rabbits who tell the same number into a color group.

For color groups who has `i+1` rabbits, we can count how many rabbits who tell `i other rabbits`. Then we can count what the minimum number of groups That can include all `i+1` rabbits. The maximum size of each group is `i+1` rabbits.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)