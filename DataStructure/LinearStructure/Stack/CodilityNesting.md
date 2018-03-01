# Codility. Nesting

### Codility

## Question

A string S consisting of N characters is called properly nested if:

* S is empty;
* S has the form "(U)" where U is a properly nested string;
* S has the form "VW" where V and W are properly nested strings.

For example, string "(()(())())" is properly nested but string "())" isn't.

Write a function:

`int solution(string &S);`

that, given a string S consisting of N characters, returns 1 if string S is properly nested and 0 otherwise.

For example, given S = "(()(())())", the function should return 1 and given S = "())", the function should return 0, as explained above.

**Assume that:**

* N is an integer within the range [0..1,000,000];
* string S consists only of the characters "(" and/or ")".

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(1) (not counting the storage required for input arguments).

## Solutions

* C++1
```
int solution(string &S) {
    int left = 0;
    for(char c : S)
    {
        if(c=='(') left++;
        else if(--left < 0) return 0;
    }
    return left==0 ? 1 : 0;
}
```

**Testcase**
```
negative_match 
invalid structure, but the number of parentheses matches

empty 
empty string

simple_grouped 
simple grouped positive and negative test, length=22

small_random

large1 
simple large positive and negative test, 10K or 10K+1 ('s followed by 10K )'s

large_full_ternary_tree 
tree of the form T=(TTT) and depth 11, length=177K+

multiple_full_binary_trees 
sequence of full trees of the form T=(TT), depths [1..10..1], with/without unmatched ')' at the end, length=49K+

broad_tree_with_deep_paths 
string of the form (TTT...T) of 300 T's, each T being '(((...)))' nested 200-fold, length=1 million
```

## Explanation

It's like push '(' into a stack, when meet a ')', remove one '(' from the stack.

Finally, only if the stack is empty, the input is properly nested.

* **worst-case time complexity:** O(N), where `N` is the length of the input.
* **worst-case space complexity:** O(1)