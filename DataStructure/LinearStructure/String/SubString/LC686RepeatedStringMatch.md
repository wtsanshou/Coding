# LC686. Repeated String Match

### LeetCode

## Question

Given two strings A and B, find the minimum number of times A has to be repeated such that B is a substring of it. If no such solution, return -1.

For example, with A = "abcd" and B = "cdabcdab".

Return 3, because by repeating A three times (“abcdabcdabcd”), B is a substring of it; and B is not a substring of A repeated two times ("abcdabcd").

**Note:**

The length of A and B will be between 1 and 10000.

## Solutions

* C#1 (Memory Limit Exceeded)
```
public int RepeatedStringMatch(string A, string B) {
    int na=A.Length, nb=B.Length;
    if(na==nb && A.Equals(B)) return 1;
    int rep = (int)Math.Ceiling((double)nb / (double)na);
    string gross = A;
    bool firstTime = true;
    for(int i=1; i<rep; ++i)
        gross += A;
    for(int i=0; i<gross.Length; ++i){
        if(i+nb>gross.Length && firstTime){
            firstTime = false;
            gross += A;
            rep++;
        }
        if(i+nb>gross.Length) return -1;
        string sub = gross.Substring(i, nb);
        if(sub.Equals(B)) return rep;
    }
    return -1;
}
```

* C#2 (Memory Limit Exceeded)
```
public class Solution {
    public int RepeatedStringMatch(string A, string B) {
        int na=A.Length, nb=B.Length;
        if(na==nb && A.Equals(B)) return 1;
        int rep = (int)Math.Ceiling((double)nb / (double)na);
        string gross = A;
        bool firstTime = true;
        for(int i=1; i<rep; ++i)
            gross += A;
        for(int i=0; i<gross.Length; ++i){
            if(i+nb>gross.Length && firstTime){
                firstTime = false;
                gross += A;
                rep++;
            }
            if(i+nb>gross.Length) return -1;
            if(isEqual(gross, i, B)) return rep;
        }
        return -1;
    }
    
    private bool isEqual(string gross, int s, string B){
        for(int i=0; i<B.Length; ++i){
            if(gross[s+i] != B[i])
                return false;
        }
        return true;
    }
}
```

* C#3 
```
public int RepeatedStringMatch(string A, string B) {
    int na=A.Length, nb=B.Length;
    for(int i=0; i<na; ++i){
        int ai=i, bi=0, rep=1;
        for(; bi<nb; ++bi){
            if(ai==na) {
                ai = 0;
                rep++;
            }
            if(A[ai++] != B[bi]) break;
        }
        if(bi == nb) return rep;
    }
    return -1;
}
```

## Explanation

The first two solutions, I tried to match substring. So I prepared the whole string of repeated A for B. This is why of the Memory Limit Exceeded.

The solution 3 meets the requirements. I compare starting from each element of A with the whole string of B. If meet the end of A, go back to the beginning of A.

* **worst-case time complexity:** O(m*n)
* **worst-case space complexity:** O(1)
