# LC384. Shuffle an Array

### LeetCode

## Question

Shuffle a set of numbers without duplicates.

**Example:**
```
// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
```

```
/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * vector<int> param_1 = obj.reset();
 * vector<int> param_2 = obj.shuffle();
 */
```

## Solutions

### Solution 1

* C++ (232ms)
```
class Solution {
private:
    vector<int> ori;
public:
    Solution(vector<int> nums) {
        ori = nums;
    }
    
    /** Resets the array to its original configuration and return it. */
    vector<int> reset() {
        return ori;
    }
    
    /** Returns a random shuffling of the array. */
    vector<int> shuffle() {
        vector<int> res = ori;
        for(int i=1; i<res.size(); ++i)
            swap(res[i], res[rand()%(i+1)]);
        return res;
    }
};
```

* Java
```
public class Solution {
    
    private int[] oriArray;
    private Random rand;
    private int size;
    
    public Solution(int[] nums) {
        oriArray = nums;
        size = nums.length;
        rand = new Random();
    }
    
    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return oriArray;
    }
    
    /** Returns a random shuffling of the array. */
    public int[] shuffle() {
        int[] shufArray = Arrays.copyOf(oriArray, size);
        for(int i=1; i<size; ++i)
        {
            int r = rand.nextInt(i+1);
            int temp = shufArray[i];
            shufArray[i] = shufArray[r];
            shufArray[r] = temp;
        }
        return shufArray;
    }
}
```

For the method shuffle(), `swap(nums[i], a random element left of nums[i])`

* **worst-case time complexity:** `O(n)`, where 'n' is the length of `nums`.
* **worst-case space complexity:** `O(n)`, where 'n' is the length of `nums`.

### Solution 2

* C++
```
class Solution {
private: 
    vector<int> nums;
public:
    Solution(vector<int> nums) {
        this->nums = nums;
    }
    
    /** Resets the array to its original configuration and return it. */
    vector<int> reset() {
        return nums;
    }
    
    /** Returns a random shuffling of the array. */
    vector<int> shuffle() {
        vector<int> result = nums;
        for(int i=0; i<result.size(); ++i)
        {
            int pos = rand()%(result.size()-i);
            swap(result[i+pos], result[i]);
        }
        return result;
    }
};
```

* Java
```
public class Solution {
    
    private int[] oriArray;
    private Random rand;
    private int size;
    
    public Solution(int[] nums) {
        oriArray = nums;
        size = nums.length;
        rand = new Random();
    }
    
    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return oriArray;
    }
    
    /** Returns a random shuffling of the array. */
    public int[] shuffle() {
        int[] shufArray = Arrays.copyOf(oriArray, size);
        for(int i=0; i<size; ++i)
        {
            int r = rand.nextInt(size - i);
            int temp = shufArray[i];
            shufArray[i] = shufArray[i+r];
            shufArray[i+r] = temp;
        }
        return shufArray;
    }
}
```

For the method shuffle(), `swap(nums[i], a random element right of nums[i])`

* **worst-case time complexity:** `O(n)`, where 'n' is the length of `nums`.
* **worst-case space complexity:** `O(n)`, where 'n' is the length of `nums`.
