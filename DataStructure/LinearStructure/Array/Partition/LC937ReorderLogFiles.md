# LC937. Reorder Log Files

### LeetCode

## Question

You have an array of logs.  Each log is a space delimited string of words.

For each log, the first word in each log is an alphanumeric identifier.  Then, either:

Each word after the identifier will consist only of lowercase letters, or;
Each word after the identifier will consist only of digits.
We will call these two varieties of logs letter-logs and digit-logs.  It is guaranteed that each log has at least one word after its identifier.

Reorder the logs so that all of the letter-logs come before any digit-log.  The letter-logs are ordered lexicographically ignoring identifier, with the identifier used in case of ties.  The digit-logs should be put in their original order.

Return the final order of the logs.

**Example 1:**
```
Input: ["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]
Output: ["g1 act car","a8 act zoo","ab1 off key dog","a1 9 2 3 1","zo4 4 7"]
```

**Note:**

* 0 <= logs.length <= 100
* 3 <= logs[i].length <= 100
* logs[i] is guaranteed to have an identifier, and a word after the identifier.

## Solutions

* Scala1
```
object Solution {
    def reorderLogFiles(logs: Array[String]): Array[String] = {
        val (left, right) = logs.partition(log => (log.charAt(indexOfTheFirstWord(log))).isLetter)
        val sortedLeft = left.sortBy(log => log.substring(indexOfTheFirstWord(log)))
        sortedLeft ++ right               
    }
    
    def indexOfTheFirstWord(log: String): Int = {
        log.indexOf(" ")+1
    }
}
```

## Explanation

1. Partition the array to [letter array, digit array];
2. Sort the `letter array`
3. Combine them.

* **worst-case time complexity:** `O(N*M)`, where `N` is the number of logs, `M` is the number of words in the log.
* **worst-case space complexity:** `O(N*M)`, where `N` is the number of logs, `M` is the number of words in the log.
