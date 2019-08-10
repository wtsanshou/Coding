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

## Questions

* <a href="LC209MinimumSizeSubarraySum.md">LC209. Minimum Size Subarray Sum</a>