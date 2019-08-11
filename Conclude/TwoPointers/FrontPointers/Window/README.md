# Window Pointers

## Template

```
for (int i = 0; i < n; i++) {
    while (j < n) {
        if (meet the condition) {
            j++;
            update state;
        } else {
            break;
        }
    }

    update state;
}
```

## Conclude

1. Two loop
2. No need to put `j` back.
3. If checking repeating characters, think of hash map.

## Questions

* <a href="LC209MinimumSizeSubarraySum.md">LC209. Minimum Size Subarray Sum</a>
* <a href="LC3LongestSubstringWithoutRepeatingCharacters.md">LC3. Longest Substring Without Repeating Characters</a>
* <a href="LC76MinimumWindowSubstring.md">LC76. Minimum Window Substring</a>
* <a href="LC19RemoveNthNodeFromEndOfList.md">LC19. Remove Nth Node From End of List</a>
