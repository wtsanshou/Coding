# LC984. String Without AAA or BBB

### LeetCode

## Question

Given two integers A and B, return any string S such that:

S has length A + B and contains exactly A 'a' letters, and exactly B 'b' letters;

The substring 'aaa' does not occur in S;

The substring 'bbb' does not occur in S.

**Example 1:**
```
Input: A = 1, B = 2
Output: "abb"
Explanation: "abb", "bab" and "bba" are all correct answers.
```

**Example 2:**
```
Input: A = 4, B = 1
Output: "aabaa"
``` 

**Note:**

* 0 <= A <= 100
* 0 <= B <= 100
* It is guaranteed such an S exists for the given A and B.

## Solutions
* Scala1
```
def strWithout3a3b(A: Int, B: Int): String = {
    var result = Array[String]()
    var a=A
    var b=B
    while(a>0 && b>0){
        if(a==b){
            result = result ++: Array.fill[String](a)("ab")
            a=0
            b=0
        }else if(a > b){
            result = result :+ "aab"
            a=a-2
            b=b-1
        }else {
            result = result :+ "bba"
            a=a-1
            b=b-2
        }
    }
    (result ++: Array.fill[String](a)("a") ++: Array.fill[String](b)("b")).mkString
}
```

## Explanation

1. If `A==B`, we just need number of `ab` string.
2. If `A!=B`, we need to put some `aab` or `bba` to reduce the larger one until `A==B`, then we can go back to 1.

* **worst-case time complexity:** `O(max(A,B))`.
* **worst-case space complexity:** `O(max(A,B))`.
