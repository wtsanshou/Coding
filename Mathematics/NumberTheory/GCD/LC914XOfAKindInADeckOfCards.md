# LC914. X of a Kind in a Deck of Cards

### LeetCode

## Question

In a deck of cards, each card has an integer written on it.

Return true if and only if you can choose X >= 2 such that it is possible to split the entire deck into 1 or more groups of cards, where:

Each group has exactly X cards.
All the cards in each group have the same integer.

**Example 1:**
```
Input: [1,2,3,4,4,3,2,1]
Output: true
Explanation: Possible partition [1,1],[2,2],[3,3],[4,4]
```

**Example 2:**
```
Input: [1,1,1,2,2,2,3,3]
Output: false
Explanation: No possible partition.
```

**Example 3:**
```
Input: [1]
Output: false
Explanation: No possible partition.
```

**Example 4:**
```
Input: [1,1]
Output: true
Explanation: Possible partition [1,1]
```

**Example 5:**
```
Input: [1,1,2,2,2,2]
Output: true
Explanation: Possible partition [1,1],[2,2],[2,2]
```

**Note:**

* 1 <= deck.length <= 10000
* 0 <= deck[i] < 10000

## Solutions

* Scala1
```
object Solution {
    def hasGroupsSizeX(deck: Array[Int]): Boolean = {
        val deckSet = deck.toSet
        if(deck.size == deckSet.size) return false
        val sizes = deckSet.map(d => deck.count(_ == d))
        val min = sizes.min
        sizes.forall(gcd(_, min) > 1) //or// !sizes.exists(gcd(_, min) == 1)
    }
    
    def gcd(a: Int, b: Int): Int = {
        if(b==0) a else gcd(b, a%b)
    }
}
```

* Scala2
```
object Solution {
    def hasGroupsSizeX(deck: Array[Int]): Boolean = {
        val groups : Map[Int, Array[Int]] = deck.groupBy(d => d)
        if(deck.size == groups.size) return false
        val sizes = groups.map(m => m._2.size).toSet
        val min = sizes.min
        sizes.forall(gcd(_, min) > 1)
    }
    
    def gcd(a: Int, b: Int): Int = {
        if(b==0) a else gcd(b, a%b)
    }
}
```

## Explanation

1. Group the elements in the `deck` by the same value. 
2. Count the size of each group.
3. When the `GDC` of each pair of sizes is more than `1`, it fullfill the requirements.

* **worst-case time complexity:** O(n), where `n` is the size of the Array `deck`.
* **worst-case space complexity:** O(n), where `n` is the size of the Array `deck`.
