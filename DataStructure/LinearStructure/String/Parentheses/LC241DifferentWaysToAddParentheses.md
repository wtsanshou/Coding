# LC241. Different Ways to Add Parentheses

### LeetCode

## Question

Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are `+`, `-` and `*`.

**Example 1**

```
Input: "2-1-1".
((2-1)-1) = 0
(2-(1-1)) = 2
Output: [0, 2]
```

**Example 2**

```
Input: "2*3-4*5"
(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10
Output: [-34, -14, -10, -10, 10]
```

## Solutions

### Solution 1

* C++ (9ms)
```
vector<int> diffWaysToCompute(string input) {
    vector<int> res;
    for(int i=0; i<input.length(); ++i)
    {
        char c = input[i];
        if(ispunct(c))
            for(auto a : diffWaysToCompute(input.substr(0, i)))
                for(auto b : diffWaysToCompute(input.substr(i+1)))
                    res.push_back(c=='+' ? a+b : (c=='-') ? a-b : a*b);
    }
    return res.size()==0 ? vector<int>{stoi(input)} : res;
}
```

* Java
```
public List<Integer> diffWaysToCompute(String input) {
    List<Integer> res = new LinkedList<Integer>();
    for(int i=0; i<input.length(); ++i)
    {
        char ch = input.charAt(i);
        if(!Character.isDigit(ch))
        {
            String left = input.substring(0, i);
            String right = input.substring(i+1, input.length());
            for(int a : diffWaysToCompute(left))
                for(int b : diffWaysToCompute(right))
                    res.add((ch == '+') ? a+b :
                            (ch == '-') ? a-b :
                                          a*b);
        }
    }
    if(res.size() == 0)
        res.add(Integer.parseInt(input));
    return res;
}
```

* Java
```
public List<Integer> diffWaysToCompute(String input) {
    List<Integer> res = new ArrayList<>();
    for(int i=0; i<input.length(); i++){
        int operator = input.charAt(i);
        if(!Character.isDigit(operator)){
            for(int left : diffWaysToCompute(input.substring(0, i))){
                for(int right : diffWaysToCompute(input.substring(i+1, input.length()))){
                    res.add(operator=='+' ? left+right : (operator=='-') ? left-right : left*right);
                }
            }
        }
    }
    return (res.isEmpty())? Arrays.asList(Integer.valueOf(input)) : res;
}
```

It use the `Divide and Conquer`. Suppose the left and right side sub-results of an operator have already obtained by the recursion of `diffWaysToCompute(String subInput)`, we can traversal the two sub-results to get the full-results.

**Complexity:**

* **worst-case time complexity:** O(n<sup>3</sup>), where `n` is the length of the `input`.
* **worst-case space complexity:** O(n<sup>3</sup>), where `n` is the length of the `input`.
