# Backpack

## Features

1. Value is the index in `DP`
2. `DP` process is filling the matrix
3. Can use `Roll Optimize`

## Finite & Infinite

There are two type of Backpack question

1. The number of each element in the Backpack is **limisted**. In this case, we need one more dimension to remember the number of the used elements. If we want to reduce the dimension, we may be able to reduce the dimension by doing the second loop from big value (`target`) to small value (`a element`).
2. The number of each element in the Backpack is **infinite**. In this case, we do the second loop from small value (`a element`) to big value (`target`). It does not need on dimension to remember the number of the used elements.

## Question

### Finite

* <a href="Finite/Lint92Backpack.md">Lint92. Backpack</a>
* <a href="Finite/563BackpackV.md">563. Backpack V</a>
* <a href="Finite/Lint798BackpackVII.md">Lint798. Backpack VII</a>
* <a href="Finite/Lint1538CardGameII.md">Lint1538. Card Game II</a>

### Infinite

* <a href="Infinite/LC322CoinChange.md">LC322. Coin Change</a>
* <a href="Infinite/Lint440BackpackIII.md">Lint440. Backpack III</a>
* <a href="Infinite/Lint562BackpackIV.md">Lint562. Backpack IV</a>


