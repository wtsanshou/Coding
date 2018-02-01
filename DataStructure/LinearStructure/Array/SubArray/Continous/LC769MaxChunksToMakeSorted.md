# LC769. Max Chunks To Make Sorted

### LeetCode

## Question

Given an array arr that is a permutation of [0, 1, ..., arr.length - 1], we split the array into some number of "chunks" (partitions), and individually sort each chunk.  After concatenating them, the result equals the sorted array.

What is the most number of chunks we could have made?

**Example 1:**
```
Input: arr = [4,3,2,1,0]
Output: 1
```

**Explanation:**

Splitting into two or more chunks will not return the required result.
For example, splitting into [4, 3], [2, 1, 0] will result in [3, 4, 0, 1, 2], which isn't sorted.

**Example 2:**
```
Input: arr = [1,0,2,3,4]
Output: 4
```

**Explanation:**

We can split into two chunks, such as [1, 0], [2, 3, 4].

However, splitting into [1, 0], [2], [3], [4] is the highest number of chunks possible.

**Note:**

* arr will have length in range [1, 10].
* arr[i] will be a permutation of [0, 1, ..., arr.length - 1].

## Solutions
* Java1
```
class Solution {
    public int maxChunksToSorted(int[] arr) {
        int n = arr.length, res=0, right=0;
        boolean[] sort = new boolean[n];
        for(int i=0, j=0; i<n; ++i){
            while(sort[j]) j++;
            sort[arr[i]] = true;
            if(arr[i] == j && isChunkFull(j, right, sort))
                res++;
            if(arr[i] > right) right = arr[i];
        }
        return res;
    }
    
    private boolean isChunkFull(int left, int right, boolean[] sort){
        for(int i=left; i<=right; ++i)
            if(!sort[i]) return false;
        return true;
    }
}
```

## Explanation

We have to find the chunks from left to right onle after another. To find a chunks, we need to find the minimum not appared number in the chunk, keep the maximum number of the chunk, and check if the chunk is full. Then move to the next chunk.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n)