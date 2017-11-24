# LC292. Nim Game

### LeetCode

## Question

You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.

Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.

**Hint:**

* If there are 5 stones in the heap, could you figure out a way to remove the stones such that you will always be the winner?

## Solutions

* C++1
```
bool canWinNim(int n) {
    return n%4!=0;
}
```

* Python1
```
def canWinNim(self, n):
    return bool(n&3)
```

## Explanation

If `n%4==0`, the other person can always find a way to remove to the position `n-4` (when n >= 4)

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(1)