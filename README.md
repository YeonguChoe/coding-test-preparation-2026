# Coding Test Preparation 2026

## Range queries
- prefix sum array

## Complete search

### Generating subsets

### Generating permutations

### Backtracking

## Graph traversal

### DFS (Depth-first search)

- Connectivity check

- Finding cycles

### BFS (Breadth-first search)

## 1D dynamic programming

### Longest increasing subsequence

## 2D dynamic programming

### 0-1 knapsack problem

#### maximize sum of values
- `row`: current available item types
- `column`: current weight capacity limit
- `memo[row][column]`: maximum value that can be created using currently available items (row) with weight limit up to current weight capacity (column).

```
if there are no available items:
    memo[0][column] = 0
if recently added item's weight > current weight capacity:
    memo[row][column] = memo[row-1][column]
if recently added item's weight <= current weight capacity:
    memo[row][column] = max(memo[row-1][column],memo[row-1][column - recently added item's weight] + recently added item's value)
```

- `m[row-1][column]`: not using recently added item
- `m[row-1][column - weight of newly added item]`: using one recently added item

```python
def zero_one_knapsack_max_value_sum(n, w, v, W):
    m = [[0 for _ in range(W + 1)] for _ in range(n + 1)]
    for i in range(1, n + 1):
        for w_i in range(W + 1):
            if w[i - 1] > w_i:
                m[i][w_i] = m[i - 1][w_i]
            if w[i - 1] <= w_i:
                m[i][w_i] = max(m[i - 1][w_i], m[i - 1][w_i - w[i - 1]] + v[i - 1])
    return m[n][W]
```

### Edit distance

- When changing word1 (row) to word2 (column)

```python
word1 = "abd"
word2 = "abc"

distance = [
    # "" a b c 
    [0, 1, 2, 3], # ""
    [1, 0, 0, 0], # a
    [2, 0, 0, 0], # b
    [3, 0, 0, 0]  # d
]
```

- insert: `distance(a-1,b)` + 1
    - `distance(a-1,b)`: state before adding the last character to word1
    - `1`: insert new character to `x[a-1]`
- delete: 1 + `distance(a,b-1)`
    - `distance(a,b-1)`: state after deleting the last character from word1
    - `1`: delete the last character from x[:a]
- edit: `distance(a-1,b-1)` + cost for changing last character
- match: `distance(a-1,b-1)`


- `distance(a,b)` = min(`insert`, `delete`, `edit`, `match`)

### Lattice Path