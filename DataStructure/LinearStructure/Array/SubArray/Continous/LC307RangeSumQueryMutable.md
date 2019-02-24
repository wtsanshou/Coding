# LC307. Range Sum Query – Mutable

### LeetCode

## Question

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.
The update(i, val) function modifies nums by updating the element at index i to val.

**Example:**
```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```

**Note:**
* 1.  The array is only modifiable by the update function.
* 2.  You may assume the number of calls to update and sumRange function is distributed evenly.

## Solutions

```
/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```

### Solution 1

* C++ (TLE)
```
class NumArray {
private: 
    vector<int> nums;
    vector<int> sums;
public:
    NumArray(vector<int> nums) {
        this->nums = nums;
        sums = vector<int>(nums.size()+1);
        for(int i=nums.size()-1; i>=0; --i)
            sums[i] = nums[i] + sums[i+1];
    }
    
    void update(int i, int val) {
        int change = val - nums[i];
        nums[i] = val;
        for(int k=i; k>=0; --k)
            sums[k] += change;
    }
    
    int sumRange(int i, int j) {
        return sums[i] - sums[j+1];
    }
};
```

See question <a href="LC303RangeSumQueryImmutable.md">LC303. Range Sum Query – Immutable</a>

* **update worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.

### Solution 2 (Segment tree) 

* Java [Accepted]
```
class NumArray {

    private int[] tree;
    private int n;

    public NumArray(int[] nums) {
        n = nums.length;
        if(n>0){
            tree = new int[2*n];
            buildTree(nums);
        }
    }
    
    public void update(int i, int val) {
        int position = i+n;
        tree[position] = val;
        while(position > 0){
            int left = position;
            int right = position;
            if(position % 2 == 0)
                right++;
            else
                left--;
            //update parent
            tree[position/2] = tree[left] + tree[right];
            position /= 2;
        }
    }
    
    public int sumRange(int i, int j) {
        i += n;
        j += n;
        int sum = 0;
        while(i <= j){
            if(i % 2 == 1)
                sum += tree[i++];
            if(j % 2 == 0)
                sum += tree[j--];
            i /= 2;
            j /= 2;
        }
        return sum;
    }
    
    private void buildTree(int[] nums){
        for(int i=n, j=0; i<2*n; ++i, ++j)
            tree[i] = nums[j];
        for(int i=n-1; i>0; --i)
            tree[i] = tree[2*i] + tree[2*i + 1]; //left is even, right is odd
    }
}
```

<a href="https://en.wikipedia.org/wiki/Segment_tree">Segment tree</a> is a very flexible data structure, because it is used to solve numerous range query problems like finding minimum, maximum, sum, greatest common divisor, least common denominator in array in logarithmic time.

![LC307. Range Sum Query – Mutable](Images/LC307RangeSumQueryMutable.png)

Segment tree could be implemented using either an array or a tree. For an array implementation, if the element at index i is not a leaf, its left and right child are stored at index 2i and 2i+1 respectively.

#### Build segment tree

We can put all leaf nodes in the range [n, 2*n-1]. Then, based on these leaf nodes, calculate their parent nodes from `n-1` to `1`.

* **update worst-case time complexity:** `O(n)`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.

#### Update segment tree

When we update the array at some index `i` we need to rebuild the segment tree, because there are tree nodes which contain the sum of the modified element. Again we will use a bottom-up approach. We update the leaf node that stores `a[i]`. From there we will follow the path up to the root updating the value of each parent as a sum of its children values.

* **update worst-case time complexity:** `O(log(n))`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`.

### Range Sum Query

Sum all right values of the left edge `i` and all left values of the right edge `j`.

* **update worst-case time complexity:** `O(log(n))`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(1)`.

### Solution 3

* C++
```
class NumArray {
private:
    vector<int> BIT;
    vector<int> Nums;
public:
    NumArray(vector<int> &nums){
        int n = nums.size();
        Nums = nums;
        //BIT = vector<int>(n+1);
        BIT.resize(n+1);
        for(int i=0; i<n; ++i)
        {
            updateBIT(i, nums[i]);
        }
    }

    void update(int i, int val) {
        if(val != Nums[i])
        {
            updateBIT(i, val-Nums[i]);
            Nums[i] = val;
        }
    }

    int sumRange(int i, int j) {
        return leftSum(j) - leftSum(i-1);
    }
    
    int leftSum(int i)
    {
        i++;
        int sum=0;
        while(i>0)
        {
            sum += BIT[i];
            i -= i & (-i);
        }
        return sum;
    }
    
    void updateBIT(int i, int val)
    {
        i++;
        while(i<BIT.size())
        {
            BIT[i] +=val;
            i += i & (-i); //double the last bit
        }
    }
};
```

Binary Indexed Trees (<a href="https://www.topcoder.com/community/data-science/data-science-
tutorials/binary-indexed-trees/">BIT or Fenwick tree</a>):

Example: given an array a[0]...a[7], we use a array BIT[9] to
represent a tree, where index [2] is the parent of [1] and [3], [6]
is the parent of [5] and [7], [4] is the parent of [2] and [6], and
[8] is the parent of [4]. I.e.,

BIT[] as a binary tree:

```
           ______________*
           ______*
           __*     __*
           *   *   *   *
indices: 0 1 2 3 4 5 6 7 8
```

BIT[i] = ([i] is a left child) ? the partial sum from its left most
descendant to itself : the partial sum from its parent (exclusive) to
itself. (check the range of "__").

```
Eg. BIT[1]=a[0], BIT[2]=a[1]+BIT[1]=a[1]+a[0], BIT[3]=a[2],
BIT[4]=a[3]+BIT[3]+BIT[2]=a[3]+a[2]+a[1]+a[0],
BIT[6]=a[5]+BIT[5]=a[5]+a[4],
BIT[8]=a[7]+BIT[7]+BIT[6]+BIT[4]=a[7]+a[6]+...+a[0], ...
```

Thus, to update a[1]=BIT[2], we shall update BIT[2], BIT[4], BIT[8],
i.e., for current [i], the next update [j] is j=i+(i&-i) //double the
last 1-bit from [i].

Similarly, to get the partial sum up to a[6]=BIT[7], we shall get the
sum of BIT[7], BIT[6], BIT[4], i.e., for current [i], the next
summand [j] is j=i-(i&-i) // delete the last 1-bit from [i].

To obtain the original value of a[7] (corresponding to index [8] of
BIT), we have to subtract BIT[7], BIT[6], BIT[4] from BIT[8], i.e.,
starting from [idx-1], for current [i], the next subtrahend [j] is
j=i-(i&-i), up to j==idx-(idx&-idx) exclusive. (However, a quicker
way but using extra space is to store the original array.)



