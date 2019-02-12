# LC989. Add to Array-Form of Integer

### LeetCode

## Question

For a non-negative integer X, the array-form of X is an array of its digits in left to right order.  For example, if X = 1231, then the array form is [1,2,3,1].

Given the array-form A of a non-negative integer X, return the array-form of the integer X+K.

**Example 1:**
```
Input: A = [1,2,0,0], K = 34
Output: [1,2,3,4]
Explanation: 1200 + 34 = 1234
```

**Example 2:**
```
Input: A = [2,7,4], K = 181
Output: [4,5,5]
Explanation: 274 + 181 = 455
```

**Example 3:**
```
Input: A = [2,1,5], K = 806
Output: [1,0,2,1]
Explanation: 215 + 806 = 1021
```

**Example 4:**
```
Input: A = [9,9,9,9,9,9,9,9,9,9], K = 1
Output: [1,0,0,0,0,0,0,0,0,0,0]
Explanation: 9999999999 + 1 = 10000000000
``` 

**Note：**

* 1 <= A.length <= 10000
* 0 <= A[i] <= 9
* 0 <= K <= 10000
* If A.length > 1, then A[0] != 0

## Solutions

### Solution 1

* Scala (3076 ms, 67.2 MB)
```
object Solution {
    def addToArrayForm(A: Array[Int], K: Int): List[Int] = {
        val k = getArray(K)
        addTwoArrays(A, k)
    }
    
    def getArray(K: Int): Array[Int] = {
        var k = K
        var arr = List[Int]()
        while(k > 0){
            arr = (k%10) +: arr
            k /= 10
        }
        arr.toArray
    }
    
    def addTwoArrays(A: Array[Int], K: Array[Int]): List[Int] = {
        var result = List[Int]()
        var (i, j) = (A.length-1, K.length-1)
        var temp = 0
        while(i>=0 || j>=0){
            val a = if(i>=0) A(i) else 0
            val k = if(j>=0) K(j) else 0
            result = (a+k+temp)%10 +: result
            temp = (a+k+temp)/10
            i -= 1
            j -= 1
        }
        if(temp>0) temp+:result else result
    }
}
```

Convert the K to an array. Add the two arrays together.

* **worst-case time complexity:** `O(N+M)`, where `N` is the length of `A`, `M` is the number of digit in `K`.
* **worst-case space complexity:** `O(N+M)`, where `N` is the length of `A`, `M` is the number of digit in `K`.

### Solution 2

* Scala (3148 ms    61.8 MB)
```
def addToArrayForm(A: Array[Int], K: Int): List[Int] = {
    var k = K
    var result = List[Int]()
    A.reverse.foreach(a => {
        result = (a+k)%10 +: result
        k = (a+k)/10
    })
    
    while(k > 0){
        result = k%10 +: result
        k /= 10
    }
    result
}
```

Similar idea as the solution 1, but using `K` itself as the `temp`.

* **worst-case time complexity:** `O(N+M)`, where `N` is the length of `A`, `M` is the number of digit in `K`.
* **worst-case space complexity:** `O(N+M)`, where `N` is the length of `A`, `M` is the number of digit in `K`.
