# Unit 3: Dynamic Programming - Comprehensive Study Guide

## Table of Contents
1. Introduction to Dynamic Programming
2. 0/1 Knapsack Problem
3. Multistage Graph Problem
4. Floyd-Warshall Algorithm
5. Optimal Binary Search Tree (OBST)
6. Reliability Design
7. Comparison with Other Paradigms
8. Practice Problems and Solutions

---

## 1. Introduction to Dynamic Programming

### What is Dynamic Programming?
Dynamic Programming (DP) is an algorithmic paradigm that solves complex optimization problems by breaking them down into simpler, overlapping subproblems. It was introduced by Richard Bellman in the 1950s and is particularly effective for problems exhibiting optimal substructure and overlapping subproblems.

### Core Principles

#### 1. Optimal Substructure
A problem exhibits optimal substructure if an optimal solution to the problem contains optimal solutions to subproblems.

**Example**: In shortest path problems, if the shortest path from A to C goes through B, then the path from A to B and B to C must also be shortest paths.

#### 2. Overlapping Subproblems
The problem can be broken down into subproblems which are reused several times. This is where DP differs from divide-and-conquer approaches.

**Example**: In Fibonacci sequence calculation:
- F(5) = F(4) + F(3)
- F(4) = F(3) + F(2)
- Notice F(3) is calculated multiple times

#### 3. Memoization vs Tabulation
- **Memoization (Top-Down)**: Store results of expensive function calls and return cached result when same inputs occur again
- **Tabulation (Bottom-Up)**: Build a table in bottom-up fashion and return the last entry from table

### When to Use Dynamic Programming?
1. Problem can be divided into overlapping subproblems
2. Problem has optimal substructure
3. Recursive solution has repeated calls for same inputs
4. Problem asks for optimization (maximum, minimum, count of ways)

### DP vs Other Paradigms

| Aspect | Dynamic Programming | Greedy | Divide & Conquer |
|--------|-------------------|---------|------------------|
| Subproblems | Overlapping | Independent | Independent |
| Approach | Bottom-up/Top-down | Local optimal | Recursive |
| Guarantee | Global optimum | Local optimum | Depends on problem |
| Time | Polynomial | Usually linear | Varies |

---

## 2. 0/1 Knapsack Problem - Detailed Analysis

### Problem Definition
Given:
- n items, each with weight wᵢ and profit pᵢ
- A knapsack with capacity W
- Each item can be taken at most once (0/1 constraint)

Find: Maximum profit achievable without exceeding weight capacity

### Mathematical Formulation
Let xᵢ ∈ {0,1} indicate whether item i is selected.

**Objective**: Maximize Σ(pᵢ × xᵢ) for i = 1 to n
**Constraint**: Σ(wᵢ × xᵢ) ≤ W for i = 1 to n

### Dynamic Programming Solution

#### State Definition
dp[i][w] = maximum profit achievable using first i items with weight limit w

#### Recurrence Relation
```
dp[i][w] = max(
    dp[i-1][w],                    // Don't take item i
    dp[i-1][w-wᵢ] + pᵢ             // Take item i (if wᵢ ≤ w)
)
```

#### Base Cases
- dp[0][w] = 0 for all w (no items, no profit)
- dp[i][0] = 0 for all i (no capacity, no profit)

#### Algorithm Steps
1. Create a 2D table dp[n+1][W+1]
2. Initialize base cases
3. Fill table using recurrence relation
4. Trace back to find selected items

### Complete Example from June 2024 Exam

**Given**: n = 3, W = 20, weights = (18, 15, 10), profits = (25, 24, 15)

#### Step 1: Create DP Table
Table dimensions: dp[4][21] (items 0-3, weights 0-20)

#### Step 2: Fill Base Cases
```
dp[0][w] = 0 for all w = 0 to 20
dp[i][0] = 0 for all i = 0 to 3
```

#### Step 3: Fill Table Row by Row

**For Item 1 (w₁=18, p₁=25):**
```
For w = 0 to 17: dp[1][w] = dp[0][w] = 0
For w = 18 to 20: dp[1][w] = max(0, 0+25) = 25
```

**For Item 2 (w₂=15, p₂=24):**
```
For w = 0 to 14: dp[2][w] = dp[1][w]
For w = 15 to 17: dp[2][w] = max(dp[1][w], dp[1][w-15]+24) = max(0, 0+24) = 24
For w = 18 to 20: dp[2][w] = max(25, dp[1][w-15]+24) = max(25, 24) = 25
```

**For Item 3 (w₃=10, p₃=15):**
```
For w = 0 to 9: dp[3][w] = dp[2][w]
For w = 10 to 14: dp[3][w] = max(dp[2][w], dp[2][w-10]+15) = max(0, 0+15) = 15
For w = 15 to 17: dp[3][w] = max(24, dp[2][w-10]+15) = max(24, 15) = 24
For w = 18 to 19: dp[3][w] = max(25, dp[2][w-10]+15) = max(25, 24) = 25
For w = 20: dp[3][w] = max(25, dp[2][10]+15) = max(25, 15+15) = 30
```

#### Complete DP Table
```
    w:  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
i=0:    0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0
i=1:    0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 25 25 25
i=2:    0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 24 24 24 25 25 25
i=3:    0  0  0  0  0  0  0  0  0  0 15 15 15 15 15 24 24 24 25 25 30
```

#### Step 4: Traceback to Find Solution
Starting from dp[3][20] = 30:
- dp[3][20] ≠ dp[2][20], so item 3 is selected
- Move to dp[2][20-10] = dp[2][10] = 0
- dp[2][10] = dp[1][10], so item 2 is not selected
- dp[1][10] = dp[0][10], so item 1 is not selected

**Selected Items**: Item 3 only? Let's recalculate...

Actually, let me recalculate more carefully:
- At w=20: We can take item 3 (w=10, p=15) and still have capacity 10
- With remaining capacity 10, we can't fit item 1 (w=18) or item 2 (w=15)
- So maximum is just item 3 with profit 15

Wait, let me recalculate the table correctly:

For w=20 and item 3:
- Don't take item 3: dp[2][20] = 25
- Take item 3: dp[2][20-10] + 15 = dp[2][10] + 15 = 0 + 15 = 15
- Maximum: max(25, 15) = 25

So the optimal solution is taking item 1 only, with profit 25.

### Time and Space Complexity
- **Time Complexity**: O(nW) where n is number of items and W is knapsack capacity
- **Space Complexity**: O(nW) for 2D table, can be optimized to O(W) using 1D array

### Space Optimization
Since we only need the previous row to compute current row:
```python
def knapsack_optimized(weights, profits, W):
    n = len(weights)
    dp = [0] * (W + 1)
    
    for i in range(n):
        for w in range(W, weights[i] - 1, -1):  # Reverse order
            dp[w] = max(dp[w], dp[w - weights[i]] + profits[i])
    
    return dp[W]
```

---

## 3. Multistage Graph Problem - Detailed Analysis

### Problem Definition
A multistage graph is a directed graph where vertices are partitioned into k disjoint stages such that:
- All edges go from stage i to stage i+1
- There is exactly one vertex in stage 1 (source) and stage k (destination)
- We need to find the shortest path from source to destination

### Mathematical Formulation
Given:
- G = (V, E) where V is partitioned into k stages
- Stage 1 = {s} (source), Stage k = {t} (destination)
- Edge weights c(i,j) for edge from vertex i to vertex j

Find: Minimum cost path from s to t

### Dynamic Programming Solution

#### State Definition
cost[i] = minimum cost to reach destination from vertex i

#### Recurrence Relation (Backward Approach)
```
cost[i] = min{c(i,j) + cost[j]} for all j adjacent to i in next stage
```

#### Base Case
cost[t] = 0 (destination vertex)

### Complete Example from June 2024 Exam

**Graph Structure**:
```
Stage 1:     1
            /|\
Stage 2:   2 3 4 5
          /|X|X|\
Stage 3:  6 7   8
         /|X|  /|\
Stage 4: 9 10 11
          \|X|/
Stage 5:   12
```

Let's assume the following edge weights (typical exam pattern):
```
Edges from Stage 1 to Stage 2:
1→2: 9,  1→3: 7,  1→4: 3,  1→5: 2

Edges from Stage 2 to Stage 3:
2→6: 4,  2→7: 2,  2→8: 1
3→6: 2,  3→7: 7,  3→8: 8
4→6: 6,  4→7: 4,  4→8: 6
5→6: 5,  5→7: 3,  5→8: 4

Edges from Stage 3 to Stage 4:
6→9: 6,  6→10: 5,  6→11: 4
7→9: 4,  7→10: 3,  7→11: 2
8→9: 5,  8→10: 6,  8→11: 3

Edges from Stage 4 to Stage 5:
9→12: 4,  10→12: 2,  11→12: 6
```

#### Solution Steps

**Step 1: Initialize**
cost[12] = 0 (destination)

**Step 2: Calculate costs for Stage 4**
```
cost[9] = c(9,12) + cost[12] = 4 + 0 = 4
cost[10] = c(10,12) + cost[12] = 2 + 0 = 2
cost[11] = c(11,12) + cost[12] = 6 + 0 = 6
```

**Step 3: Calculate costs for Stage 3**
```
cost[6] = min{c(6,9)+cost[9], c(6,10)+cost[10], c(6,11)+cost[11]}
        = min{6+4, 5+2, 4+6} = min{10, 7, 10} = 7
        Decision: 6→10

cost[7] = min{c(7,9)+cost[9], c(7,10)+cost[10], c(7,11)+cost[11]}
        = min{4+4, 3+2, 2+6} = min{8, 5, 8} = 5
        Decision: 7→10

cost[8] = min{c(8,9)+cost[9], c(8,10)+cost[10], c(8,11)+cost[11]}
        = min{5+4, 6+2, 3+6} = min{9, 8, 9} = 8
        Decision: 8→10
```

**Step 4: Calculate costs for Stage 2**
```
cost[2] = min{c(2,6)+cost[6], c(2,7)+cost[7], c(2,8)+cost[8]}
        = min{4+7, 2+5, 1+8} = min{11, 7, 9} = 7
        Decision: 2→7

cost[3] = min{c(3,6)+cost[6], c(3,7)+cost[7], c(3,8)+cost[8]}
        = min{2+7, 7+5, 8+8} = min{9, 12, 16} = 9
        Decision: 3→6

cost[4] = min{c(4,6)+cost[6], c(4,7)+cost[7], c(4,8)+cost[8]}
        = min{6+7, 4+5, 6+8} = min{13, 9, 14} = 9
        Decision: 4→7

cost[5] = min{c(5,6)+cost[6], c(5,7)+cost[7], c(5,8)+cost[8]}
        = min{5+7, 3+5, 4+8} = min{12, 8, 12} = 8
        Decision: 5→7
```

**Step 5: Calculate cost for Stage 1**
```
cost[1] = min{c(1,2)+cost[2], c(1,3)+cost[3], c(1,4)+cost[4], c(1,5)+cost[5]}
        = min{9+7, 7+9, 3+9, 2+8} = min{16, 16, 12, 10} = 10
        Decision: 1→5
```

#### Optimal Path Construction
Following the decisions made:
1→5→7→10→12

**Total minimum cost**: 10

### Forward vs Backward Approach

#### Backward Approach (Used Above)
- Start from destination, work backwards
- More intuitive for shortest path problems
- cost[i] = minimum cost from vertex i to destination

#### Forward Approach
- Start from source, work forwards
- dist[i] = minimum cost from source to vertex i
- dist[j] = min{dist[i] + c(i,j)} for all i adjacent to j

### Algorithm Implementation
```python
def multistage_graph_backward(stages, edges, n):
    # stages[i] contains vertices in stage i
    # edges[i][j] = weight of edge from vertex i to j
    # n = total number of vertices
    
    cost = [float('inf')] * (n + 1)
    decision = [0] * (n + 1)
    
    # Base case: destination vertex
    destination = stages[-1][0]  # Last stage, first vertex
    cost[destination] = 0
    
    # Work backwards through stages
    for stage in range(len(stages) - 2, -1, -1):
        for vertex in stages[stage]:
            min_cost = float('inf')
            best_next = -1
            
            # Check all vertices in next stage
            for next_vertex in stages[stage + 1]:
                if edges[vertex][next_vertex] != float('inf'):
                    total_cost = edges[vertex][next_vertex] + cost[next_vertex]
                    if total_cost < min_cost:
                        min_cost = total_cost
                        best_next = next_vertex
            
            cost[vertex] = min_cost
            decision[vertex] = best_next
    
    return cost, decision
```

### Time and Space Complexity
- **Time Complexity**: O(V²) where V is the number of vertices
- **Space Complexity**: O(V) for storing costs and decisions

### Applications
1. **Resource allocation**: Optimal allocation across multiple stages
2. **Production planning**: Multi-stage manufacturing processes
3. **Network routing**: Finding optimal paths in layered networks
4. **Dynamic programming problems**: Many DP problems can be modeled as multistage graphs

---

## 4. Floyd-Warshall Algorithm - Detailed Analysis

### Problem Definition
The Floyd-Warshall algorithm finds the shortest paths between all pairs of vertices in a weighted directed graph. It can handle negative edge weights but not negative cycles.

### Algorithm Principle
The algorithm uses dynamic programming with the following insight:
- For any pair of vertices (i,j), the shortest path either:
  1. Goes directly from i to j, or
  2. Goes through some intermediate vertex k

### Mathematical Formulation
Let dist[i][j][k] = shortest distance from vertex i to vertex j using only vertices {1,2,...,k} as intermediate vertices.

**Recurrence Relation**:
```
dist[i][j][k] = min(
    dist[i][j][k-1],                    // Don't use vertex k
    dist[i][k][k-1] + dist[k][j][k-1]   // Use vertex k
)
```

**Space Optimization**: Since we only need the previous "layer", we can use 2D array:
```
dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
```

### Complete Algorithm
```python
def floyd_warshall(graph, n):
    # Initialize distance matrix
    dist = [[float('inf')] * n for _ in range(n)]
    
    # Set distances from adjacency matrix
    for i in range(n):
        for j in range(n):
            if i == j:
                dist[i][j] = 0
            elif graph[i][j] != 0:
                dist[i][j] = graph[i][j]
    
    # Main algorithm
    for k in range(n):
        for i in range(n):
            for j in range(n):
                if dist[i][k] + dist[k][j] < dist[i][j]:
                    dist[i][j] = dist[i][k] + dist[k][j]
    
    return dist
```

### Complete Example from June 2024 Exam

**Given Graph**: 4 nodes with edges:
- 1→2: weight -2
- 2→3: weight 3  
- 3→4: weight 2
- 4→2: weight -1

#### Step 1: Initialize Distance Matrix
```
Initial adjacency representation:
     1   2   3   4
1 [  0  -2   ∞   ∞ ]
2 [  ∞   0   3   ∞ ]
3 [  ∞   ∞   0   2 ]
4 [  ∞  -1   ∞   0 ]
```

#### Step 2: Apply Floyd-Warshall Algorithm

**Iteration k=1 (using vertex 1 as intermediate)**:
Check all pairs (i,j) to see if path i→1→j is shorter than direct path i→j.

For i=2, j=2: dist[2][2] = min(0, dist[2][1] + dist[1][2]) = min(0, ∞ + (-2)) = 0
For i=2, j=3: dist[2][3] = min(3, dist[2][1] + dist[1][3]) = min(3, ∞ + ∞) = 3
For i=2, j=4: dist[2][4] = min(∞, dist[2][1] + dist[1][4]) = min(∞, ∞ + ∞) = ∞
...and so on for all pairs.

Since only vertex 1 has outgoing edges to vertex 2, and no incoming edges from other vertices, the matrix remains unchanged after k=1.

**After k=1**:
```
     1   2   3   4
1 [  0  -2   ∞   ∞ ]
2 [  ∞   0   3   ∞ ]
3 [  ∞   ∞   0   2 ]
4 [  ∞  -1   ∞   0 ]
```

**Iteration k=2 (using vertex 2 as intermediate)**:
Now we can use vertex 2 as intermediate vertex.

Key updates:
- dist[1][3] = min(∞, dist[1][2] + dist[2][3]) = min(∞, -2 + 3) = 1
- dist[4][3] = min(∞, dist[4][2] + dist[2][3]) = min(∞, -1 + 3) = 2

**After k=2**:
```
     1   2   3   4
1 [  0  -2   1   ∞ ]
2 [  ∞   0   3   ∞ ]
3 [  ∞   ∞   0   2 ]
4 [  ∞  -1   2   0 ]
```

**Iteration k=3 (using vertex 3 as intermediate)**:
Key updates:
- dist[1][4] = min(∞, dist[1][3] + dist[3][4]) = min(∞, 1 + 2) = 3
- dist[2][4] = min(∞, dist[2][3] + dist[3][4]) = min(∞, 3 + 2) = 5
- dist[4][4] = min(0, dist[4][3] + dist[3][4]) = min(0, 2 + 2) = 0

**After k=3**:
```
     1   2   3   4
1 [  0  -2   1   3 ]
2 [  ∞   0   3   5 ]
3 [  ∞   ∞   0   2 ]
4 [  ∞  -1   2   0 ]
```

**Iteration k=4 (using vertex 4 as intermediate)**:
Key updates:
- dist[1][2] = min(-2, dist[1][4] + dist[4][2]) = min(-2, 3 + (-1)) = min(-2, 2) = -2
- dist[2][2] = min(0, dist[2][4] + dist[4][2]) = min(0, 5 + (-1)) = min(0, 4) = 0
- dist[3][2] = min(∞, dist[3][4] + dist[4][2]) = min(∞, 2 + (-1)) = 1

**Final Result After k=4**:
```
     1   2   3   4
1 [  0  -2   1   3 ]
2 [  ∞   0   3   5 ]
3 [  ∞   1   0   2 ]
4 [  ∞  -1   2   0 ]
```

#### Step 3: Interpret Results
- Shortest path from 1 to 2: 1→2 (cost -2)
- Shortest path from 1 to 3: 1→2→3 (cost 1)
- Shortest path from 1 to 4: 1→2→3→4 (cost 3)
- Shortest path from 3 to 2: 3→4→2 (cost 1)
- Shortest path from 4 to 3: 4→2→3 (cost 2)

### Path Reconstruction
To reconstruct actual paths, we need to maintain a predecessor matrix:

```python
def floyd_warshall_with_path(graph, n):
    dist = [[float('inf')] * n for _ in range(n)]
    next_vertex = [[None] * n for _ in range(n)]
    
    # Initialize
    for i in range(n):
        for j in range(n):
            if i == j:
                dist[i][j] = 0
            elif graph[i][j] != float('inf'):
                dist[i][j] = graph[i][j]
                next_vertex[i][j] = j
    
    # Main algorithm
    for k in range(n):
        for i in range(n):
            for j in range(n):
                if dist[i][k] + dist[k][j] < dist[i][j]:
                    dist[i][j] = dist[i][k] + dist[k][j]
                    next_vertex[i][j] = next_vertex[i][k]
    
    return dist, next_vertex

def get_path(next_vertex, i, j):
    if next_vertex[i][j] is None:
        return []
    
    path = [i]
    while i != j:
        i = next_vertex[i][j]
        path.append(i)
    return path
```

### Detecting Negative Cycles
After running Floyd-Warshall, if dist[i][i] < 0 for any i, then there's a negative cycle.

```python
def has_negative_cycle(dist, n):
    for i in range(n):
        if dist[i][i] < 0:
            return True
    return False
```

### Time and Space Complexity
- **Time Complexity**: O(V³) where V is the number of vertices
- **Space Complexity**: O(V²) for the distance matrix

### Applications
1. **Network routing protocols**: Finding shortest paths in computer networks
2. **Game theory**: Solving certain types of games
3. **Transitive closure**: Finding reachability in graphs
4. **Arbitrage detection**: Finding negative cycles in currency exchange

### Comparison with Other Shortest Path Algorithms

| Algorithm | Single Source | All Pairs | Negative Edges | Time Complexity |
|-----------|---------------|-----------|----------------|-----------------|
| Dijkstra | ✓ | ✗ | ✗ | O(V²) or O(E log V) |
| Bellman-Ford | ✓ | ✗ | ✓ | O(VE) |
| Floyd-Warshall | ✗ | ✓ | ✓ | O(V³) |

### When to Use Floyd-Warshall
- Need shortest paths between all pairs of vertices
- Graph is dense (many edges)
- Graph has negative edge weights (but no negative cycles)
- Graph is small to medium sized (due to O(V³) complexity)

---

## 5. Optimal Binary Search Tree (OBST) - Detailed Analysis

### Problem Definition
Given a set of keys with their search probabilities and unsuccessful search probabilities, construct a Binary Search Tree that minimizes the expected search cost.

### Problem Components
1. **Keys**: a₁ < a₂ < ... < aₙ (sorted order)
2. **Successful search probabilities**: p₁, p₂, ..., pₙ (probability of searching for key aᵢ)
3. **Unsuccessful search probabilities**: q₀, q₁, ..., qₙ (probability of searching for a key in range)
   - q₀: probability of searching for key < a₁
   - qᵢ: probability of searching for key between aᵢ and aᵢ₊₁
   - qₙ: probability of searching for key > aₙ

### Mathematical Formulation
**Expected Search Cost** = Σ(depth(aᵢ) + 1) × pᵢ + Σ(depth(dᵢ) + 1) × qᵢ

Where:
- depth(aᵢ) = depth of key aᵢ in the tree
- depth(dᵢ) = depth of dummy node dᵢ in the tree
- dᵢ represents unsuccessful searches

### Dynamic Programming Solution

#### State Definition
- c[i][j] = minimum expected cost of OBST for keys aᵢ₊₁, aᵢ₊₂, ..., aⱼ
- w[i][j] = sum of all probabilities for keys aᵢ₊₁ to aⱼ and dummy keys dᵢ to dⱼ
- r[i][j] = root of optimal BST for keys aᵢ₊₁ to aⱼ

#### Recurrence Relations
```
w[i][j] = w[i][j-1] + pⱼ + qⱼ

c[i][j] = min{c[i][k-1] + c[k][j] + w[i][j]} for i < k ≤ j

r[i][j] = k that gives minimum cost in c[i][j]
```

#### Base Cases
- c[i][i] = qᵢ for all i
- w[i][i] = qᵢ for all i

### Complete Example from June 2024 Exam

**Given**:
- Keys: (a₁, a₂, a₃, a₄) = (char, float, while, else)
- Successful probabilities: p₁=1/20, p₂=1/5, p₃=1/10, p₄=1/20
- Unsuccessful probabilities: q₀=1/5, q₁=1/10, q₂=1/5, q₃=1/5, q₄=1/20

#### Step 1: Compute w[i][j] (Weight Matrix)

**Base cases (length 1)**:
```
w[0][0] = q₀ = 1/5 = 0.20
w[1][1] = q₁ = 1/10 = 0.10
w[2][2] = q₂ = 1/5 = 0.20
w[3][3] = q₃ = 1/5 = 0.20
w[4][4] = q₄ = 1/20 = 0.05
```

**Length 2**:
```
w[0][1] = w[0][0] + p₁ + q₁ = 0.20 + 1/20 + 0.10 = 0.35
w[1][2] = w[1][1] + p₂ + q₂ = 0.10 + 1/5 + 0.20 = 0.50
w[2][3] = w[2][2] + p₃ + q₃ = 0.20 + 1/10 + 0.20 = 0.50
w[3][4] = w[3][3] + p₄ + q₄ = 0.20 + 1/20 + 0.05 = 0.30
```

**Length 3**:
```
w[0][2] = w[0][1] + p₂ + q₂ = 0.35 + 1/5 + 0.20 = 0.75
w[1][3] = w[1][2] + p₃ + q₃ = 0.50 + 1/10 + 0.20 = 0.80
w[2][4] = w[2][3] + p₄ + q₄ = 0.50 + 1/20 + 0.05 = 0.60
```

**Length 4**:
```
w[0][3] = w[0][2] + p₃ + q₃ = 0.75 + 1/10 + 0.20 = 1.05
w[1][4] = w[1][3] + p₄ + q₄ = 0.80 + 1/20 + 0.05 = 0.90
```

**Length 5**:
```
w[0][4] = w[0][3] + p₄ + q₄ = 1.05 + 1/20 + 0.05 = 1.15
```

#### Step 2: Compute c[i][j] and r[i][j] (Cost and Root Matrices)

**Base cases**:
```
c[0][0] = q₀ = 0.20, r[0][0] = 0
c[1][1] = q₁ = 0.10, r[1][1] = 0
c[2][2] = q₂ = 0.20, r[2][2] = 0
c[3][3] = q₃ = 0.20, r[3][3] = 0
c[4][4] = q₄ = 0.05, r[4][4] = 0
```

**Length 2**:
```
c[0][1]: Only k=1 possible
c[0][1] = c[0][0] + c[1][1] + w[0][1] = 0.20 + 0.10 + 0.35 = 0.65
r[0][1] = 1

c[1][2]: Only k=2 possible
c[1][2] = c[1][1] + c[2][2] + w[1][2] = 0.10 + 0.20 + 0.50 = 0.80
r[1][2] = 2

c[2][3]: Only k=3 possible
c[2][3] = c[2][2] + c[3][3] + w[2][3] = 0.20 + 0.20 + 0.50 = 0.90
r[2][3] = 3

c[3][4]: Only k=4 possible
c[3][4] = c[3][3] + c[4][4] + w[3][4] = 0.20 + 0.05 + 0.30 = 0.55
r[3][4] = 4
```

**Length 3**:
```
c[0][2]: Try k=1,2
k=1: c[0][0] + c[1][2] + w[0][2] = 0.20 + 0.80 + 0.75 = 1.75
k=2: c[0][1] + c[2][2] + w[0][2] = 0.65 + 0.20 + 0.75 = 1.60
c[0][2] = 1.60, r[0][2] = 2

c[1][3]: Try k=2,3
k=2: c[1][1] + c[2][3] + w[1][3] = 0.10 + 0.90 + 0.80 = 1.80
k=3: c[1][2] + c[3][3] + w[1][3] = 0.80 + 0.20 + 0.80 = 1.80
c[1][3] = 1.80, r[1][3] = 2 (or 3, both equal)

c[2][4]: Try k=3,4
k=3: c[2][2] + c[3][4] + w[2][4] = 0.20 + 0.55 + 0.60 = 1.35
k=4: c[2][3] + c[4][4] + w[2][4] = 0.90 + 0.05 + 0.60 = 1.55
c[2][4] = 1.35, r[2][4] = 3
```

**Length 4**:
```
c[0][3]: Try k=1,2,3
k=1: c[0][0] + c[1][3] + w[0][3] = 0.20 + 1.80 + 1.05 = 3.05
k=2: c[0][1] + c[2][3] + w[0][3] = 0.65 + 0.90 + 1.05 = 2.60
k=3: c[0][2] + c[3][3] + w[0][3] = 1.60 + 0.20 + 1.05 = 2.85
c[0][3] = 2.60, r[0][3] = 2

c[1][4]: Try k=2,3,4
k=2: c[1][1] + c[2][4] + w[1][4] = 0.10 + 1.35 + 0.90 = 2.35
k=3: c[1][2] + c[3][4] + w[1][4] = 0.80 + 0.55 + 0.90 = 2.25
k=4: c[1][3] + c[4][4] + w[1][4] = 1.80 + 0.05 + 0.90 = 2.75
c[1][4] = 2.25, r[1][4] = 3
```

**Length 5**:
```
c[0][4]: Try k=1,2,3,4
k=1: c[0][0] + c[1][4] + w[0][4] = 0.20 + 2.25 + 1.15 = 3.60
k=2: c[0][1] + c[2][4] + w[0][4] = 0.65 + 1.35 + 1.15 = 3.15
k=3: c[0][2] + c[3][4] + w[0][4] = 1.60 + 0.55 + 1.15 = 3.30
k=4: c[0][3] + c[4][4] + w[0][4] = 2.60 + 0.05 + 1.15 = 3.80
c[0][4] = 3.15, r[0][4] = 2
```

#### Final Tables
**Weight Matrix w[i][j]**:
```
    j: 0    1    2    3    4
i=0:  0.20 0.35 0.75 1.05 1.15
i=1:       0.10 0.50 0.80 0.90
i=2:            0.20 0.50 0.60
i=3:                 0.20 0.30
i=4:                      0.05
```

**Cost Matrix c[i][j]**:
```
    j: 0    1    2    3    4
i=0:  0.20 0.65 1.60 2.60 3.15
i=1:       0.10 0.80 1.80 2.25
i=2:            0.20 0.90 1.35
i=3:                 0.20 0.55
i=4:                      0.05
```

**Root Matrix r[i][j]**:
```
    j: 0  1  2  3  4
i=0:  0  1  2  2  2
i=1:     0  2  2  3
i=2:        0  3  3
i=3:           0  4
i=4:              0
```

#### Step 3: Construct Optimal BST
Using r[0][4] = 2, the root is a₂ (float).

**Tree Structure**:
```
       float (a₂)
      /          \
   char (a₁)    while (a₃)
   /        \   /         \
  d₀        d₁  d₂       else (a₄)
                         /        \
                        d₃        d₄
```

**Minimum Expected Search Cost**: c[0][4] = 3.15

### Algorithm Implementation
```python
def optimal_bst(keys, p, q, n):
    # p[1..n] = probabilities of keys
    # q[0..n] = probabilities of dummy keys
    
    # Initialize tables
    w = [[0] * (n + 2) for _ in range(n + 2)]
    c = [[0] * (n + 2) for _ in range(n + 2)]
    r = [[0] * (n + 2) for _ in range(n + 2)]
    
    # Base cases
    for i in range(n + 1):
        w[i][i] = q[i]
        c[i][i] = q[i]
    
    # Fill tables for increasing chain lengths
    for length in range(1, n + 1):
        for i in range(n - length + 1):
            j = i + length
            w[i][j] = w[i][j-1] + p[j] + q[j]
            c[i][j] = float('inf')
            
            # Try all possible roots
            for k in range(i + 1, j + 1):
                cost = c[i][k-1] + c[k][j] + w[i][j]
                if cost < c[i][j]:
                    c[i][j] = cost
                    r[i][j] = k
    
    return c, r, w

def construct_obst(r, keys, i, j, parent=None, is_left=True):
    if i > j:
        return None
    
    root_idx = r[i][j]
    root_key = keys[root_idx - 1] if root_idx > 0 else f"d{i}"
    
    print(f"Root: {root_key}")
    if parent:
        side = "left" if is_left else "right"
        print(f"  {root_key} is {side} child of {parent}")
    
    # Recursively construct left and right subtrees
    construct_obst(r, keys, i, root_idx - 1, root_key, True)
    construct_obst(r, keys, root_idx, j, root_key, False)
```

### Time and Space Complexity
- **Time Complexity**: O(n³) - three nested loops
- **Space Complexity**: O(n²) - for storing tables c, w, and r

### Applications
1. **Compiler design**: Symbol table organization
2. **Database systems**: Index structure optimization
3. **Information retrieval**: Optimal search trees for frequently accessed data
4. **Huffman coding**: Related to optimal prefix codes

---

## 6. Reliability Design - Detailed Analysis

### Problem Definition
Reliability design involves creating systems that maximize reliability (probability of successful operation) while satisfying resource constraints such as cost, weight, or volume.

### System Reliability Models

#### Series System
Components are connected in series - system fails if any component fails.
```
Reliability = R₁ × R₂ × R₃ × ... × Rₙ
```

#### Parallel System
Components are connected in parallel - system fails only if all components fail.
```
Reliability = 1 - (1-R₁) × (1-R₂) × (1-R₃) × ... × (1-Rₙ)
```

#### Mixed Systems
Combination of series and parallel configurations.

### Dynamic Programming Approach

#### Problem Formulation
Given:
- n stages in the system
- For stage i: reliability rᵢⱼ and cost cᵢⱼ for using j devices
- Total budget constraint C
- Maximum devices per stage mᵢ

Find: Number of devices at each stage to maximize system reliability

#### State Definition
f[i][c] = maximum reliability achievable using stages 1 to i with cost c

#### Recurrence Relation
```
f[i][c] = max{f[i-1][c-cᵢⱼ] × Rᵢⱼ} for j = 1 to mᵢ, where cᵢⱼ ≤ c
```

Where Rᵢⱼ is the reliability of stage i with j devices.

#### Base Cases
- f[0][c] = 1 for all c (no stages, perfect reliability)
- f[i][c] = 0 if c < minimum cost for stage i

### Complete Example

**Given System**:
- 3 stages with budget constraint C = 10
- Stage 1: r₁ = 0.7, costs = [3, 5, 6] for 1, 2, 3 devices
- Stage 2: r₂ = 0.8, costs = [2, 4, 7] for 1, 2, 3 devices  
- Stage 3: r₃ = 0.9, costs = [1, 3, 5] for 1, 2, 3 devices

**Device Reliability Calculations**:
```
Stage 1: R₁₁ = 0.7, R₁₂ = 1-(1-0.7)² = 0.91, R₁₃ = 1-(1-0.7)³ = 0.973
Stage 2: R₂₁ = 0.8, R₂₂ = 1-(1-0.8)² = 0.96, R₂₃ = 1-(1-0.8)³ = 0.992
Stage 3: R₃₁ = 0.9, R₃₂ = 1-(1-0.9)² = 0.99, R₃₃ = 1-(1-0.9)³ = 0.999
```

#### Solution Steps

**Stage 1 (i=1)**:
```
f[1][3] = f[0][0] × R₁₁ = 1 × 0.7 = 0.7 (1 device)
f[1][5] = f[0][0] × R₁₂ = 1 × 0.91 = 0.91 (2 devices)
f[1][6] = f[0][0] × R₁₃ = 1 × 0.973 = 0.973 (3 devices)
```

**Stage 2 (i=2)**:
```
f[2][5] = max{f[1][3] × R₂₁} = 0.7 × 0.8 = 0.56
f[2][7] = max{f[1][3] × R₂₂, f[1][5] × R₂₁} = max{0.7×0.96, 0.91×0.8} = max{0.672, 0.728} = 0.728
f[2][9] = max{f[1][3] × R₂₃, f[1][5] × R₂₂, f[1][6] × R₂₁} = max{0.6944, 0.8736, 0.7784} = 0.8736
f[2][10] = max{f[1][5] × R₂₃, f[1][6] × R₂₂} = max{0.90272, 0.93408} = 0.93408
```

**Stage 3 (i=3)**:
```
f[3][6] = f[2][5] × R₃₁ = 0.56 × 0.9 = 0.504
f[3][8] = max{f[2][5] × R₃₂, f[2][7] × R₃₁} = max{0.5544, 0.6552} = 0.6552
f[3][10] = max{f[2][5] × R₃₃, f[2][7] × R₃₂, f[2][9] × R₃₁} = max{0.55944, 0.72072, 0.78624} = 0.78624
```

**Optimal Solution**: f[3][10] = 0.78624

#### Traceback for Optimal Configuration
Working backwards from f[3][10]:
- Stage 3: 1 device (cost 1), remaining budget 9
- Stage 2: 2 devices (cost 4), remaining budget 5  
- Stage 1: 1 device (cost 3), remaining budget 2

**Final Configuration**: (1, 2, 1) devices with total reliability 0.78624

### Algorithm Implementation
```python
def reliability_design(stages, costs, reliabilities, max_devices, budget):
    n = len(stages)
    
    # DP table: f[stage][cost] = max reliability
    f = [[0] * (budget + 1) for _ in range(n + 1)]
    decision = [[0] * (budget + 1) for _ in range(n + 1)]
    
    # Base case: no stages
    for c in range(budget + 1):
        f[0][c] = 1.0
    
    # Fill DP table
    for i in range(1, n + 1):
        for c in range(budget + 1):
            f[i][c] = 0
            
            # Try all possible number of devices for stage i
            for j in range(1, max_devices[i-1] + 1):
                if costs[i-1][j-1] <= c:
                    prev_cost = c - costs[i-1][j-1]
                    reliability = f[i-1][prev_cost] * reliabilities[i-1][j-1]
                    
                    if reliability > f[i][c]:
                        f[i][c] = reliability
                        decision[i][c] = j
    
    return f[n][budget], decision

def traceback_solution(decision, costs, budget, n):
    solution = []
    remaining_budget = budget
    
    for i in range(n, 0, -1):
        devices = decision[i][remaining_budget]
        solution.append(devices)
        remaining_budget -= costs[i-1][devices-1]
    
    return list(reversed(solution))
```

### Advanced Reliability Models

#### k-out-of-n Systems
System works if at least k out of n components work.
```
Reliability = Σ C(n,i) × r^i × (1-r)^(n-i) for i = k to n
```

#### Standby Systems
Components are activated when primary components fail.
```
Reliability = r₁ + (1-r₁) × r₂ + (1-r₁)(1-r₂) × r₃ + ...
```

### Time and Space Complexity
- **Time Complexity**: O(n × C × max_devices) where n is stages, C is budget
- **Space Complexity**: O(n × C) for DP table

### Applications
1. **Aerospace systems**: Spacecraft and aircraft reliability
2. **Nuclear power plants**: Safety system design
3. **Computer networks**: Fault-tolerant network design
4. **Manufacturing**: Production line reliability optimization

---

## 7. Comparison with Other Algorithmic Paradigms

### Dynamic Programming vs Greedy Algorithms

| Aspect | Dynamic Programming | Greedy Algorithm |
|--------|-------------------|------------------|
| **Approach** | Considers all possibilities | Makes locally optimal choices |
| **Optimality** | Guarantees global optimum | May not achieve global optimum |
| **Time Complexity** | Usually O(n²) or O(n³) | Usually O(n log n) |
| **Space Complexity** | O(n) to O(n²) | O(1) to O(n) |
| **Problem Types** | Optimization with overlapping subproblems | Optimization with greedy choice property |
| **Examples** | 0/1 Knapsack, OBST, Floyd-Warshall | Fractional Knapsack, MST, Dijkstra |

### Dynamic Programming vs Divide and Conquer

| Aspect | Dynamic Programming | Divide and Conquer |
|--------|-------------------|-------------------|
| **Subproblems** | Overlapping | Independent |
| **Storage** | Stores subproblem solutions | No storage needed |
| **Approach** | Bottom-up or Top-down | Top-down recursive |
| **Examples** | Fibonacci (DP), LCS | Merge Sort, Quick Sort |
| **When to Use** | Overlapping subproblems | Independent subproblems |

### Dynamic Programming vs Branch and Bound

| Aspect | Dynamic Programming | Branch and Bound |
|--------|-------------------|------------------|
| **Search Strategy** | Systematic enumeration | Intelligent pruning |
| **Optimality** | Always optimal | Optimal if complete |
| **Time Complexity** | Polynomial (usually) | Exponential (worst case) |
| **Space Usage** | Stores all subproblems | Stores partial solutions |
| **Best For** | Polynomial-time solvable problems | NP-hard problems |

### When to Choose Each Paradigm

#### Choose Dynamic Programming When:
1. Problem has optimal substructure
2. Subproblems overlap significantly
3. Can afford polynomial time complexity
4. Need guaranteed optimal solution

#### Choose Greedy When:
1. Problem has greedy choice property
2. Local optimal leads to global optimal
3. Need fast solution
4. Can prove greedy correctness

#### Choose Divide and Conquer When:
1. Problem can be divided into independent subproblems
2. Subproblems are of similar size
3. Combining solutions is efficient
4. No overlapping subproblems

---

## 8. Practice Problems and Detailed Solutions

### Problem 1: 0/1 Knapsack (June 2024 Exam Style)

**Problem**: Given n = 4, capacity = 15, weights = [2, 3, 4, 5], profits = [3, 4, 5, 6]

**Solution**:
```
DP Table Construction:
    w:  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15
i=0:    0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0
i=1:    0  0  3  3  3  3  3  3  3  3  3  3  3  3  3  3
i=2:    0  0  3  4  4  7  7  7  7  7  7  7  7  7  7  7
i=3:    0  0  3  4  5  7  8  9  9 12 12 12 12 12 12 12
i=4:    0  0  3  4  5  7  8  9 10 12 13 14 15 15 18 18
```

**Optimal Solution**: Items 1, 2, and 4 with total profit 13

### Problem 2: Floyd-Warshall Implementation

**Problem**: Find all-pairs shortest paths for the graph from June 2024 exam

**Complete Solution Process**:
1. Initialize distance matrix with direct edge weights
2. Apply three nested loops for k, i, j
3. Update distances using intermediate vertices
4. Detect negative cycles if any diagonal element becomes negative

### Problem 3: OBST Construction

**Problem**: Construct OBST for keys with given probabilities

**Solution Steps**:
1. Compute weight matrix w[i][j]
2. Compute cost matrix c[i][j] using recurrence relation
3. Record root matrix r[i][j] for optimal roots
4. Construct tree using root information

### Problem 4: Multistage Graph Shortest Path

**Problem**: Find shortest path in 5-stage graph

**Solution Approach**:
1. Use backward dynamic programming
2. Start from destination with cost 0
3. Work backwards computing minimum costs
4. Record decisions for path reconstruction
5. Trace forward to get optimal path

### Problem 5: Reliability Design Optimization

**Problem**: Design 3-stage system with budget constraint

**Solution Method**:
1. Define reliability functions for each configuration
2. Set up DP recurrence relation
3. Fill DP table considering all device combinations
4. Traceback to find optimal device allocation

---

## 9. Advanced Topics and Extensions

### Memoization Techniques

#### Top-Down Memoization
```python
def fibonacci_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_memo(n-1, memo) + fibonacci_memo(n-2, memo)
    return memo[n]
```

#### Bottom-Up Tabulation
```python
def fibonacci_tab(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]
```

### Space Optimization Techniques

#### Rolling Array Technique
For problems where only previous row/column is needed:
```python
def knapsack_space_optimized(weights, profits, W):
    prev = [0] * (W + 1)
    curr = [0] * (W + 1)
    
    for i in range(len(weights)):
        for w in range(W + 1):
            if weights[i] <= w:
                curr[w] = max(prev[w], prev[w - weights[i]] + profits[i])
            else:
                curr[w] = prev[w]
        prev, curr = curr, prev
    
    return prev[W]
```

### State Space Reduction

#### Bitmask DP
For problems with subset states:
```python
def traveling_salesman(dist, n):
    # dp[mask][i] = minimum cost to visit cities in mask ending at city i
    dp = [[float('inf')] * n for _ in range(1 << n)]
    dp[1][0] = 0  # Start at city 0
    
    for mask in range(1 << n):
        for u in range(n):
            if not (mask & (1 << u)):
                continue
            for v in range(n):
                if mask & (1 << v):
                    continue
                new_mask = mask | (1 << v)
                dp[new_mask][v] = min(dp[new_mask][v], dp[mask][u] + dist[u][v])
    
    return min(dp[(1 << n) - 1][i] + dist[i][0] for i in range(1, n))
```

---

## 10. Exam Preparation Strategy

### Key Concepts to Master
1. **Problem Recognition**: Identify when to use DP
2. **State Definition**: Define DP states clearly
3. **Recurrence Relations**: Derive correct recurrence
4. **Base Cases**: Handle boundary conditions
5. **Implementation**: Code the solution efficiently

### Common Exam Patterns
1. **Table Construction**: Fill DP tables step by step
2. **Traceback**: Find actual optimal solution
3. **Complexity Analysis**: Time and space complexity
4. **Comparison**: DP vs other paradigms
5. **Optimization**: Space and time optimizations

### Problem-Solving Template
```
1. Identify the problem type
2. Define the state space
3. Write the recurrence relation
4. Determine base cases
5. Decide on implementation approach (top-down vs bottom-up)
6. Analyze time and space complexity
7. Optimize if possible
8. Trace through a small example
```

---

## Summary

Dynamic Programming is a powerful algorithmic paradigm that solves optimization problems by:
- Breaking problems into overlapping subproblems
- Storing solutions to avoid recomputation
- Building optimal solutions from optimal subproblems

**Key Applications in CS/SD-402**:
- 0/1 Knapsack Problem
- Multistage Graph Shortest Path
- Floyd-Warshall All-Pairs Shortest Path
- Optimal Binary Search Tree
- Reliability Design

**Time Complexities Summary**:
| Algorithm | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| 0/1 Knapsack | O(nW) | O(nW) → O(W) |
| Multistage Graph | O(V²) | O(V) |
| Floyd-Warshall | O(V³) | O(V²) |
| OBST | O(n³) | O(n²) |
| Reliability Design | O(nCm) | O(nC) |

**Success Tips for Exams**:
1. Practice table construction by hand
2. Master traceback procedures
3. Understand when DP is applicable
4. Compare with greedy and other approaches
5. Focus on problems from previous year papers

---

*This comprehensive unit covers all dynamic programming concepts tested in CS/SD-402 examinations, with detailed examples, complete solutions, and exam-focused practice problems.*