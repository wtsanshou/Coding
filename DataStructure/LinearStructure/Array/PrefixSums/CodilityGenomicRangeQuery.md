# Codility. Genomic Range Query

### Codility

## Question

A DNA sequence can be represented as a string consisting of the letters A, C, G and T, which correspond to the types of successive nucleotides in the sequence. Each nucleotide has an impact factor, which is an integer. Nucleotides of types A, C, G and T have impact factors of 1, 2, 3 and 4, respectively. You are going to answer several queries of the form: What is the minimal impact factor of nucleotides contained in a particular part of the given DNA sequence?

The DNA sequence is given as a non-empty string S = S[0]S[1]...S[N-1] consisting of N characters. There are M queries, which are given in non-empty arrays P and Q, each consisting of M integers. The K-th query (0 ≤ K < M) requires you to find the minimal impact factor of nucleotides contained in the DNA sequence between positions P[K] and Q[K] (inclusive).

For example, consider string S = CAGCCTA and arrays P, Q such that:

`P[0] = 2 Q[0] = 4 P[1] = 5 Q[1] = 5 P[2] = 0 Q[2] = 6`

The answers to these M = 3 queries are as follows:

* The part of the DNA between positions 2 and 4 contains nucleotides G and C (twice), whose impact factors are 3 and 2 respectively, so the answer is 2.
* The part between positions 5 and 5 contains a single nucleotide T, whose impact factor is 4, so the answer is 4.
* The part between positions 0 and 6 (the whole string) contains all nucleotides, in particular nucleotide A whose impact factor is 1, so the answer is 1.

**Write a function:**

`vector<int> solution(string &S, vector<int> &P, vector<int> &Q);`

that, given a non-empty zero-indexed string S consisting of N characters and two non-empty zero-indexed arrays P and Q consisting of M integers, returns an array consisting of M integers specifying the consecutive answers to all queries.

The sequence should be returned as:

* a Results structure (in C), or
* a vector of integers (in C++), or
* a Results record (in Pascal), or
* an array of integers (in any other programming language).

For example, given the string S = CAGCCTA and arrays P, Q such that:

`P[0] = 2 Q[0] = 4 P[1] = 5 Q[1] = 5 P[2] = 0 Q[2] = 6`

the function should return the values [2, 4, 1], as explained above.
Assume that:

* N is an integer within the range [1..100,000];
* M is an integer within the range [1..50,000];
* each element of arrays P, Q is an integer within the range [0..N − 1];
* P[K] ≤ Q[K], where 0 ≤ K < M;
* string S consists only of upper-case English letters A, C, G, T.

Elements of input arrays can be modified.

## Solutions

### Solution 1

* C++ (100%)
```
vector<int> solution(string &S, vector<int> &P, vector<int> &Q) {
    int m = P.size(), n = S.length();
    vector<int> res(m, 4);
    vector<vector<int>> count(n+1, vector<int>(3));
    for(int i=0; i<n; ++i)
    {
        count[i+1][0] = count[i][0] + (S[i]=='A' ? 1 : 0);
        count[i+1][1] = count[i][1] + (S[i]=='C' ? 1 : 0);
        count[i+1][2] = count[i][2] + (S[i]=='G' ? 1 : 0);
    }
    for(int i=0; i<m; ++i)
    {
        for(int j=0; j<3; ++j)
            if( count[Q[i]+1][j] - count[P[i]][j] > 0)
            {
                res[i] = j+1;
                break;
            }
    }
    return res;
}
```

* Java
```
public int[] solution(String S, int[] P, int[] Q) {
    int n = S.length();
    int pqLen = P.length;
    int[] res = new int[pqLen];
    Arrays.fill(res, 4);
    int[][] count = new int[n+1][3];
    for(int i=0; i<n; ++i){
        count[i+1][0] = count[i][0] + (S.charAt(i)=='A' ? 1 : 0);
        count[i+1][1] = count[i][1] + (S.charAt(i)=='C' ? 1 : 0);
        count[i+1][2] = count[i][2] + (S.charAt(i)=='G' ? 1 : 0);
    }
    
    for(int i=0; i<pqLen; ++i){
        for(int j=0; j<3; ++j){
            int numFactor = count[Q[i]+1][j] - count[P[i]][j];
            if(numFactor > 0){
                res[i] = j+1;
                break;
            }
        }
    }
    return res;
}
```
Because `T` has the weakest impact. We can initialize the result with all `T`.
Using a `2D` array to just count the prefix `A`, `C`, and `G`. 

To find the answer of `P` and `Q`, we just need to get the count number of `A`, `C`, and `G`. When found one, set the impact factors to the result respectively.

**Complexity:**

* **worst-case time complexity:** `O(N+M)`, where `N` is length of `S`, `M` is the length of `P` or `Q`.
* **worst-case space complexity:** `O(N)`, where `N` is length of `S`.

## Testcase

extreme_sinlge 

single character string


extreme_double 

double character string


simple 

simple tests


small_length_string 

small length simple string


small_random 

small random string, length = ~300


almost_all_same_letters 

GGGGGG..??..GGGGGG..??..GGGGGG
 

large_random 

large random string, length


extreme_large 

all max ranges

