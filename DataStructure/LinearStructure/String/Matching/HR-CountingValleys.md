# HR. Counting Valleys

### HackerRank

## Question

Gary is an avid hiker. He tracks his hikes meticulously, paying close attention to small details like topography. During his last hike he took exactly `n` steps. For every step he took, he noted if it was an uphill, `U`, or a downhill, `D` step. Gary's hikes start and end at sea level and each step up or down represents a `1` unit change in altitude. We define the following terms:

* A mountain is a sequence of consecutive steps above sea level, starting with a step up from sea level and ending with a step down to sea level.
* A valley is a sequence of consecutive steps below sea level, starting with a step down from sea level and ending with a step up to sea level.

Given Gary's sequence of up and down steps during his last hike, find and print the number of valleys he walked through.

For example, if Gary's path is `DDUUUUDD`, he first enters a valley `2` units deep. Then he climbs out an up onto a mountain `2` units high. Finally, he returns to sea level and ends his hike.

**Function Description**

Complete the countingValleys function in the editor below. It must return an integer that denotes the number of valleys Gary traversed.

countingValleys has the following parameter(s):

* n: the number of steps Gary takes
* s: a string describing his path

**Input Format**

* The first line contains an integer `n`, the number of steps in Gary's hike. 
* The second line contains a single string `s`, of `n` characters that describe his path.

**Constraints**

* 2<= n <= 10<sup>6</sup>
* s[i] is {U, D}

**Output Format**

* Print a single integer that denotes the number of valleys Gary walked through during his hike.

**Sample Input**

```
8
UDDDUDUU
```

**Sample Output**
```
1
```

**Explanation**
```
If we represent _ as sea level, a step up as /, and a step down as \, Gary's hike can be drawn as:
_/\      _
   \    /
    \/\/
He enters and leaves one valley.
```

## Solutions

### Solution 1

* Java
```
static int countingValleys(int n, String s) {
    int res = 0;
    int level = 0;
    char[] sc = s.toCharArray();
    for(int i=0; i<sc.length; i++){
        int preLevel = level;
        level += (sc[i]=='U') ? 1 : -1;
        if(preLevel==0 && level==-1) res++;
    }
    return res;
}
```

A valley alwasys starting with a step down from sea level, so we just need to count how many `a step down from sea level`.

A valley also ending with a step up to sea level, so we can just count how many `ending with a step up to sea level` as well.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `s`.
