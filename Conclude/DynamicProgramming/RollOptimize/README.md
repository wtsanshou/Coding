# Roll Optimize

Sometime, the `Function` of `DP` is only related a few adjacent states. In this case, we can use **Roll Optimize** to reduce the space complexity.

## For Example

```
dp[i] = max(dp[i - 1], dp[i - 2] + A[i - 1]
            ||
            ||
            \/
dp[i % 2] = max(dp[(i - 1) % 2], dp[(i - 2) % 2] + A[i - 1])
```

## Questions

* <a href="LC198HouseRobber.md">LC198. House Robber</a>
* <a href="LC221MaximalSquare.md">LC221. Maximal Square</a>
* <a href="LC1687PaveSquare.md">LC1687. Pave Square</a>
