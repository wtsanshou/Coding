# LC553. Optimal Division

### LeetCode

## Question

Given a list of positive integers, the adjacent integers will perform the float division. For example, [2,3,4] -> 2 / 3 / 4.

However, you can add any number of parenthesis at any position to change the priority of operations. You should find out how to add parenthesis to get the `maximum result`, and return the corresponding expression in string format. `Your expression should NOT contain redundant parenthesis`.

**Example:**
```
Input: [1000,100,10,2]
Output: "1000/(100/10/2)"

Explanation:
1000/(100/10/2) = 1000/((100/10)/2) = 200
However, the bold parenthesis in "1000/((100/10)/2)" are redundant, 
since they don't influence the operation priority. So you should return "1000/(100/10/2)". 

Other cases:
1000/(100/10)/2 = 50
1000/(100/(10/2)) = 50
1000/100/10/2 = 0.5
1000/100/(10/2) = 2
```

**Note:**

1.	The length of the input array is [1, 10].
2.	Elements in the given array will be in range [2, 1000].
3.	There is only one optimal division for each test case.

## Solutions

### Solution 1

* C++
```
string optimalDivision(vector<int>& nums) {
    int n = nums.size();
    string res = to_string(nums[0]);
    if(n==1) return res;
    if(n==2) return res + "/" + to_string(nums[1]);

    res += "/(" + to_string(nums[1]);
    for(int i=2; i<n; ++i)
        res += "/" + to_string(nums[i]);
    return res + ")";
}
```

When I see the question, I came out an idea is that recursivly divided the array `nums` to two sub array like `"(" + optimalDivision(left_sub_nums) + ")" + "/" + "(" + optimalDivision(right_sub_nums) + ")"`, at the same time to check if this is the maximum result. But the requirement `Your expression should NOT contain redundant parenthesis` make it very difficult to parse the result. 

Finally, I found this is not an algorithm question, but a mathematic question. Because the `Elements in the given array will be in range [2, 1000]`, the more division the smaller the result is. 

To make a fraction the maximum, we need to keep the numerator as large as possible, keep the dinominator as smaller as possible. Therefore, the single first number is the largest numerator; the division of all the rest numbers is the smallest dinominator.

**Note** should use StringBuilder.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `nums`.