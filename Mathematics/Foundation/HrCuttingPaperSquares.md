# Hr. Cutting Paper Squares

### HackerRank

## Question

Mary has an `n×m` piece of paper that she wants to cut into `1×1` pieces according to the following rules:

* She can only cut one piece of paper at a time, meaning she cannot fold the paper or layer already-cut pieces on top of one another.
* Each cut is a straight line from one side of the paper to the other side of the paper. For example, the diagram below depicts the three possible ways to cut a `3×2`  piece of paper:  

Given n and m, find and print the minimum number of cuts Mary must make to cut the paper into `n·m` squares that are `1×1`  unit in size.

**Input Format**

A single line of two space-separated integers denoting the respective values of `n` and `m`.

**Constraints**

* 1 <= n, m <= 10<sup>9</sup>

**Output Format**

Print a long integer denoting the minimum number of cuts needed to cut the entire paper into `1×1`  squares.

**Sample Input**

```
3 1
```

**Sample Output**

```
2
```

**Explanation**

Mary first cuts the `3×1` piece of paper into a `1×1` piece and a `2×1` piece. She then cuts the `2×1`  piece into two `1×1` pieces:

Because it took her two cuts to get `n×m` =3 pieces of size `1×1`, we print 2 as our answer.

## Solutions

* Java1
```
private static long solve(int n, int m){
    return (long)n*(m-1) + (n-1);
}

public static void main(String[] args) {
    Scanner in = new Scanner(System.in);
    int n = in.nextInt();
    int m = in.nextInt();
    long result = solve(n, m);
    System.out.println(result);
}
```

## Explanation

1. Cut the paper into `n` `m x 1` pieces, we need to cut `n-1` times.
2. for each `m x 1` piece, we need to cut 'm-1' times.

So, the result is `(n-1) + n * (m-1)`

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(1)