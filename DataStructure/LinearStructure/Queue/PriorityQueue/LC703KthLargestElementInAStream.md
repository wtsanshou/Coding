# LC703. Kth Largest Element in a Stream

### LeetCode

## Question

Design a class to find the kth largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Your KthLargest class will have a constructor which accepts an integer k and an integer array nums, which contains initial elements from the stream. For each call to the method KthLargest.add, return the element representing the kth largest element in the stream.

**Example:**
```
int k = 3;
int[] arr = [4,5,8,2];
KthLargest kthLargest = new KthLargest(3, arr);
kthLargest.add(3);   // returns 4
kthLargest.add(5);   // returns 5
kthLargest.add(10);  // returns 5
kthLargest.add(9);   // returns 8
kthLargest.add(4);   // returns 8
```

**Note:**

* You may assume that nums' length ≥ k-1 and k ≥ 1.

## Solutions

* Scala1
```
class KthLargest(_k: Int, _nums: Array[Int]) {

    var numbers = collection.mutable.PriorityQueue[Int]()(Ordering.Int.reverse)
    
    _nums.foreach(addNumber(_))
    
    def add(num: Int): Int = {
        addNumber(num)
        numbers.head
    }
    
    def addNumber(num: Int): Unit = {
        numbers.enqueue(num)
        if(numbers.size > _k) numbers.dequeue()
    }

}

/**
 * Your KthLargest object will be instantiated and called as such:
 * var obj = new KthLargest(k, nums)
 * var param_1 = obj.add(`val`)
 */
```

* Java1
```
class KthLargest {

    private int k;
    private PriorityQueue<Integer> numbers;
    
    public KthLargest(int k, int[] nums) {
        this.k = k;
        numbers = new PriorityQueue<>();
        for(int n : nums){
            addNumber(n);
        }
    }
    
    public int add(int val) {
        addNumber(val);
        return numbers.peek();
    }
    
    private void addNumber(int val){
        numbers.add(val);
        if(numbers.size() > k)
            numbers.poll();
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```

## Explanation

1. Putting all edge cells into a `priority_queue` (min heap).
2. Using a `visited` to remember the visited cells.
3. Pull cell from the `priority_queue`. Traverse around the cell, if found a lower cell, put water in it `pq.push(Cell(row, col, max(cell.height, heightMap[row][col])));`. Add the number of water to result `res += max(0, cell.height-heightMap[row][col]);`.

* **worst-case time complexity:** `log(N)`, where `N` is the length of the `priorityQueue`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the `priorityQueue`.

