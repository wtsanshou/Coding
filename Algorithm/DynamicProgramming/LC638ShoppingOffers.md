# LC638. Shopping Offers

### LeetCode

## Question

In LeetCode Store, there are some kinds of items to sell. Each item has a price.

However, there are some special offers, and a special offer consists of one or more different kinds of items with a sale price.

You are given the each item's price, a set of special offers, and the number we need to buy for each item. The job is to output the lowest price you have to pay for exactly certain items as given, where you could make optimal use of the special offers.

Each special offer is represented in the form of an array, the last number represents the price you need to pay for this special offer, other numbers represents how many specific items you could get if you buy this offer.

You could use any of special offers as many times as you want.

**Example 1:**
```
Input: [2,5], [[3,0,5],[1,2,10]], [3,2]
Output: 14
```

**Explanation:**
``` 
There are two kinds of items, A and B. Their prices are $2 and $5 respectively. 
In special offer 1, you can pay $5 for 3A and 0B
In special offer 2, you can pay $10 for 1A and 2B. 
You need to buy 3A and 2B, so you may pay $10 for 1A and 2B (special offer #2), and $4 for 2A.
```

**Example 2:**
```
Input: [2,3,4], [[1,1,0,4],[2,2,1,9]], [1,2,1]
Output: 11
```

**Explanation:**
```
The price of A is $2, and $3 for B, $4 for C. 
You may pay $4 for 1A and 1B, and $9 for 2A ,2B and 1C. 
You need to buy 1A ,2B and 1C, so you may pay $4 for 1A and 1B (special offer #1), and $3 for 1B, $4 for 1C. 
You cannot add more items, though only $9 for 2A ,2B and 1C.
```
**Note:**

1.  There are at most 6 kinds of items, 100 special offers.
2.  For each item, you need to buy at most 6 of them.
3.  You are not allowed to buy more items than you want, even if that would lower the overall price.

## Solutions

* C++1
```
class Solution {
public:
    int sumPrice(vector<int>& price, vector<int>& needs)
    {
        int res = 0;
        for(int i=0; i<price.size(); ++i)
            res += price[i]*needs[i];
        return res;
    }
    
    int shoppingOffers(vector<int>& price, vector<vector<int>>& special, vector<int>& needs) {
        int res = sumPrice(price, needs);
        for(auto offer : special)
        {
            vector<int> clone(needs.begin(), needs.end());
            int i=0;
            for(; i<needs.size(); ++i)
            {
                clone[i] -= offer[i];
                if(clone[i] < 0) break;
            }
            if(i==needs.size())
                res = min(res, offer[i]+shoppingOffers(price, special, clone));
        }
        return res;
    }
};
```

* C++2
```
public:
    int sumPrice(vector<int>& price, vector<int>& needs)
    {
        int res = 0;
        for(int i=0; i<price.size(); ++i)
            res += price[i]*needs[i];
        return res;
    }
    
    int shopping(vector<int>& price, vector<vector<int>>& special, vector<int>& needs, map<vector<int>,int>& mem)
    {
        if(mem[needs]>0) return mem[needs];
        
        int res = sumPrice(price, needs);
        for(auto offer : special)
        {
            vector<int> clone(needs.begin(), needs.end());
            int i=0;
            for(; i<needs.size(); ++i)
            {
                clone[i] -= offer[i];
                if(clone[i] < 0) break;
            }
            if(i==needs.size())
                res = min(res, offer[i]+shopping(price, special, clone, mem));
        }
        mem[needs] = res;
        return res;
    }
    
    int shoppingOffers(vector<int>& price, vector<vector<int>>& special, vector<int>& needs) {
        map<vector<int>,int> mem;
        return shopping( price, special,needs, mem);
    }
};
```

* Java1
```
public class Solution {
    public int shoppingOffers(List<Integer> price, List<List<Integer>> special, List<Integer> needs) {
        Map<List<Integer>, Integer> mem = new HashMap<>();
        return shopping(price, special,needs, mem);
    }
    
    private int shopping(List<Integer> price, List<List<Integer>> special, List<Integer> needs, Map<List<Integer>, Integer> mem)
    {
        if(mem.containsKey(needs)) return mem.get(needs);
        
        int res = sumPrice(price, needs);
        for(List<Integer> offer : special)
        {
            List<Integer> clone = new ArrayList<Integer>(needs);
            int i=0;
            for(; i<needs.size(); ++i)
            {
                clone.set(i, clone.get(i) - offer.get(i));
                if(clone.get(i) < 0) break;
            }
            if(i==needs.size())
                res = Math.min(res, offer.get(i)+shopping(price, special, clone, mem));
        }
        mem.put(needs, res);
        return res;
    }

    private int sumPrice(List<Integer> price, List<Integer> needs)
    {
        int res = 0;
        for(int i=0; i<price.size(); ++i)
            res += price.get(i) * needs.get(i);
        return res;
    }
}
```

## Explanation

At the beginning, I was thinking to sort the special list by the sum of saved money of eahc offer. I even planned to put price of each item to the special list.

Then, I awared a use case: a previous offer contains few items, if we use this offer, it may destroy the next offer which contains a lot of expensive items. Therefore, Sortting is not a solution of this question.

I did try to use negative price in the input. It seems the algorithm will calculate it. Negative price is not possible in the real world. But it is not limited in the question.

The algorithm is to use every valid offer in each recursion. The minimum cost is the result.

Using a memory to save middle needs could reduce some calculation. It is **dynamic programming**.

**NOTE:** C++ can't directly use vector<int> in unordered_map.
```
Each unordered associative container is parameterized by Key, by a function object type Hash that meets the Hash requirements (17.6.3.4) and acts as a hash function for argument values of type Key, and by a binary predicate Pred that induces an equivalence relation on values of type Key.
```

Need to define hashcode for it
```
typedef vector<int> point;

class my_hash {
public:
  size_t operator()(const point &p) const {
    return boost::hash_value(p);
  }
};

// somewhere in your code, where you declare your unordered_map variable
std::unordered_map<point, int, my_hash> myUnorderedMap;
```

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n<sup>2</sup>)