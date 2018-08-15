# LC458. Poor Pigs

### LeetCode

## Question

There are 1000 buckets, one and only one of them contains poison, the rest are filled with water. They all look the same. If a pig drinks that poison it will die within 15 minutes. What is the minimum amount of pigs you need to figure out which bucket contains the poison within one hour.

Answer this question, and write an algorithm for the follow-up general case.

**Follow-up:**

If there are n buckets and a pig drinking poison will die within m minutes, how many pigs (x) you need to figure out the "poison" bucket within p minutes? There is exact one bucket with poison.

## Solutions

* Scala1
```
def poorPigs(buckets: Int, minutesToDie: Int, minutesToTest: Int): Int = {
    var pigs = 0
    while(Math.pow((minutesToTest / minutesToDie + 1), pigs) < buckets) pigs += 1
    pigs
}
```

## Explanation

If a pig drinks that poison it will die within 15 minutes. What is the minimum amount of pigs you need to figure out which bucket contains the poison within one hour.

You can try 4 times.

**1 Pig**
```
0   1   2   3   4
```

If you have one pigs, let the pig drink one bucket each time. After maximum 4 times, you can find the poison bucket in maximum 5 bucket.

If the pig die after drink the bucket `i`, you can figure out the bucket `i` with poison
If the pig alive, the last bucket has poison.

**2 Pig**
```
(0,0)   (0,1)   (0,2)   (0,3)   (0,4)
(1,0)   (1,1)   (1,2)   (1,3)   (1,4)
(2,0)   (2,1)   (2,2)   (2,3)   (2,4)
(3,0)   (3,1)   (3,2)   (3,3)   (3,4)
(4,0)   (4,1)   (4,2)   (4,3)   (4,4) 
```
If you have two pig, let one pig drink row by row 5 buckets each time, the other pig drink column by column 5 buckets each time. After maximum 4 times, you can find the poison bucket in maximum 25 bucket.

If the pigs die after drink the row `i` and column `j`, you can figure out the bucket `Array[i][j]` has poison
If only one pig die, the poisoned bucket is at `Array[i][4]` or `Array[4][j]`
If no pig die, the last bucket `Array(4,4)` has poison.

**3 Pig**

If you have three pigs, let each pig drink plane by plane 25 buckets each time from 3 different dimensionality. After maximum 4 times, you can find the poison bucket in maximum 125 bucket.

**4 Pig**

If you have three pigs, let each pig drink plane by plane 125 buckets each time from 4 different dimensionality. After maximum 4 times, you can find the poison bucket in maximum 625 bucket.

And so on ...

Conclusion:

```
Pigs    Max Buckets
1           5^1
2           5^2
3           5^3
4           5^4
5           5^5
.           .
.           .
```

Max Buckets = (minutesToTest / minutesToDie + 1)<sup>PigsNumber</sup>

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(1)
