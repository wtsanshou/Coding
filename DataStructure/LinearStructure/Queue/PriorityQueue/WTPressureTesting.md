# WT. Pressure Testing

## Question

Given an array `arr` of questions with pressure values, you can select `k` questions to answer. If the sum of the `k` questions you selected is equal or larger than the given pressure value `m`, you will feel depress.

If you can find `k` questions which makes you feel no depress, return `yes`, otherwise return `no`.

**Example 1**
```
Given: 7, 3, [5,4,3,2,1]
Return: yes
```

**Example 2**
```
Given: 7, 3, [5,4,3,2,2]
Return: no
```

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param m: the limit
     * @param k: the sum of choose
     * @param arr: the array
     * @return: yes or no
     */
    public String depress(int m, int k, int[] arr) {
        PriorityQueue<Integer> maxQuestions = new PriorityQueue<>(k+1, (a,b) -> Integer.compare(b, a));
        for(int question : arr){
            if(maxQuestions.size()>k) maxQuestions.poll();
            maxQuestions.add(question);
        }
        if(maxQuestions.size()>k) maxQuestions.poll();
        int depVal = 0;
        for(int val : maxQuestions)
            depVal += val;
        return depVal < m ? "yes" : "no";
    }
}
```

* Java
```
public String depress(int m, int k, int[] arr) {
    PriorityQueue<Integer> maxQuestions = new PriorityQueue<>(k+1, (a,b) -> Integer.compare(b, a));
    for(int question : arr){
        maxQuestions.add(question);
        if(maxQuestions.size()>k) maxQuestions.poll();
    }
    int depVal = 0;
    for(int val : maxQuestions)
        depVal += val;
    return depVal < m ? "yes" : "no";
}
```

Using the max heap to exclude high pressure questions, only left `k` minimum pressure questions.

The initial capacity of priority queue of Java will not limit you to add value into the queue. When you add values beyond the capacity, the priority queue will automatically grow its size.

**Complexity:**

* **worst-case time complexity:** `O(n * log(k))`, where `n` is the length of the `arr`, `k` is the number of questions you can select.
* **worst-case space complexity:** `O(k)`, where `k` is the number of questions you can select.
