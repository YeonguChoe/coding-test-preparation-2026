# Coding Test Preparation 2026

## Range queries
- prefix sum array

## Backtracking

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

- 2D array specification
    - cell definition: unique path from `(0, 0)` to `(i, j)`
    - 1st row and 1st column is all `1`
- dp(i,j) = dp(i-1,j)+dp(i,j-1)


### Longest Common Subsequence
- `Subsequence`: string that some characters may get deleted from original string
- `dp(r,c)` is `LCS(word1[:r],word2[:c])`
- `dp(r,c)`
    - `""` (empty string) if either word1[:r] or word2[:c] is an empty string
    - `dp(r-1,c-1) + word1[r-1]` if the last character of word1 and word2 are the same
    - longer string of `LCS(word1[:r-1],word2[:c])` and `LCS(word1[:r],word2[:c-1])` if the last character of word1 and word2 are different


#### example) word1="GAC", word2="AGCAT"
- put word1 in the row and word2 in the column
```python
dp = [
#    ""  A   G   C    A    T
    ["", "", "", "",  "",  ""],   # ""
    ["", "", "G","G", "G", "G"],  # G
    ["", "A","A","A", "A", "A"],  # A
    ["", "A","A","AC","AC","AC"], # C
]
```

### Longest Palindromic Substring

- dp(l,r): substring from left pointer (`l`) to right pointer (`r`) is palindrome
- dp(l,r)
    - `True` if it is one letter
    - `True` if s[l] == s[r] and
        - if s[l] and s[r] are next to each other
        - or if a character exists between s[l] and s[r] (e.g, `bab`)
        - or if inner substring is also palindrome `dp[l+1][r-1] == True`
    - `False` otherwise

#### example) s = "baab"

- `l` is left pointer
- `r` is right pointer

```python
dp = [
# r:  0      1      2      3      # l
    [True,  False, False, True ], # 0
    [None,  True,  True,  False], # 1
    [None,  None,  True,  False], # 2
    [None,  None,  None,  True ], # 3
]
```

- `dp` table should be filled from short substring to long substring (from substring length `0` to `len(s)-1`)
    1. `0` <= `substring_length` <= `len(s)-1`
    1. `r` = `l` + `substring_length`
    1. `l` = `r` - `substring_length`
    1. `r` <= `len(s)-1`
    1. `l` <= `len(s)-1` - `substring_length`
    



### Subset Sum Problem

### Partition Problem
- is a type of subset sum problem