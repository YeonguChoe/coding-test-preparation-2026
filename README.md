# Coding Test Preparation 2026

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

### Knapsack problem

#### 0-1 knapsack problem

##### counting possible cases
- row: available item types 
- column: weight capacity

```
memo[row][column] = table[row-1][column] + table[row][column - (recently added coin denomination)]
```

#### maximize sum of values
- `row`: current available item types
- `column`: current weight capacity limit
- `memo[row][column]`: maximum value that can be created with current weight capacity and current available items

```
if current weight capacity is zero:
    memo[row][column] = 0
if recently added item's weight > current weight capacity:
    memo[row][column] = memo[row-1][column]
if recently added item's weight <= current weight capacity:
    memo[row][column] = max(memo[row-1][column],memo[row-1][column - recently added item's weight] + recently added item's value)
```

- `m[row-1][column]`: not using newly added item
- `m[row-1][column - weight of newly added item]`: using one newly added item

#### Unbounded knapsack problem



### Edit distance

### Lattice Path