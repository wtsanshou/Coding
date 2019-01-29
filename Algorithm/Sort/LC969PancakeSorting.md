# LC969. Pancake Sorting

### LeetCode

## Question

Given an array A, we can perform a pancake flip: We choose some positive integer k <= A.length, then reverse the order of the first k elements of A.  We want to perform zero or more pancake flips (doing them one after another in succession) to sort the array A.

Return the k-values corresponding to a sequence of pancake flips that sort A.  Any valid answer that sorts the array within 10 * A.length flips will be judged as correct.

**Example 1:**
```
Input: [3,2,4,1]
Output: [4,2,4,3]
Explanation: 
We perform 4 pancake flips, with k values 4, 2, 4, and 3.
Starting state: A = [3, 2, 4, 1]
After 1st flip (k=4): A = [1, 4, 2, 3]
After 2nd flip (k=2): A = [4, 1, 2, 3]
After 3rd flip (k=4): A = [3, 2, 1, 4]
After 4th flip (k=3): A = [1, 2, 3, 4], which is sorted. 
```

**Example 2:**
```
Input: [1,2,3]
Output: []
Explanation: The input is already sorted, so there is no need to flip anything.
Note that other answers, such as [3, 3], would also be accepted.
``` 

**Note:**

* 1 <= A.length <= 100
* A[i] is a permutation of [1, 2, ..., A.length]

## Solutions

* Java1
```
class Solution {
    public List<Integer> pancakeSort(int[] A) {
        List<Integer> result = new LinkedList<>();
        for(int i=A.length; i>1; --i){
            int maxId = findMaxIn(A, i);
            result.add(maxId+1);
            reverse(A, 0, maxId);
            result.add(i);
            reverse(A, 0, i-1);
        }
        return result;
    }
    
    private int findMaxIn(int[] A, int end){
        int result = 0;
        int id = 0;
        for(int i=0; i<end; ++i)
            if(A[i] > result){
                result = A[i];
                id = i;
            }
        return id;
    }
    
    private void reverse(int[] A, int i, int j){
        while(i < j){
            int temp = A[i];
            A[i++] = A[j];
            A[j--] = temp;
        }
    }
}
```

## Explanation

The idea is to flip the maximum value to the head and flip it to the end.

The maximum number of flips is less than `2 * A.length`.

* **worst-case time complexity:** O(N<sup>2</sup>), where `N` is the length of the `A`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the `A`.
