# LC942. DI String Match

### LeetCode

## Question

Given a string S that only contains "I" (increase) or "D" (decrease), let N = S.length.

Return any permutation A of [0, 1, ..., N] such that for all i = 0, ..., N-1:

`If S[i] == "I", then A[i] < A[i+1]`

`If S[i] == "D", then A[i] > A[i+1]`

**Example 1:**
```
Input: "IDID"
Output: [0,4,1,3,2]
```

**Example 2:**
```
Input: "III"
Output: [0,1,2,3]
```

**Example 3:**
```
Input: "DDI"
Output: [3,2,0,1]
```

**Note:**

* 1 <= S.length <= 10000
* S only contains characters "I" or "D".

## Solutions

* Scala1
```
def diStringMatch(S: String): Array[Int] = {
    var (i, j) = (-1, S.length+1)
    (S+"I").toCharArray().map(c => if(c=='I'){
        i = i+1
        i
    }else{
        j = j-1
        j
    })
}
```

* Java
```
public int[] diStringMatch(String S) {
    int n = S.length();
    int[] res = new int[n+1];
    int i=0, d=n;
    for(int s=0; s<n; s++)
        res[s] = (S.charAt(s) == 'I') ? i++ : d--;
    
    res[n] = i;
    return res;
}
```

## Explanation

From left to right of the input:

`If S[i] == "I", then put the remaining minimum number`

`If S[i] == "D", then put the remaining maximum number`

* **worst-case time complexity:** O(N), where `N` is the length of the input String.
* **worst-case space complexity:** O(N), where `N` is the length of the input String.
