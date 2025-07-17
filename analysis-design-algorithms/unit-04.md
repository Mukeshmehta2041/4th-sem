# Unit 4: Backtracking, Branch & Bound, and Parallel Algorithms - Comprehensive Study Guide

## Table of Contents
1. Introduction to Backtracking
2. 8-Queens Problem
3. Hamiltonian Cycle Problem
4. Graph Coloring Problem
5. Introduction to Branch & Bound Method
6. Traveling Salesman Problem using Branch & Bound
7. Lower Bound Theory
8. Introduction to Parallel Algorithms
9. Comparison of Techniques
10. Practice Problems and Solutions

---

## 1. Introduction to Backtracking - Detailed Analysis

### What is Backtracking?
Backtracking is a systematic method for solving problems by exploring all possible solutions incrementally and abandoning ("backtracking") partial solutions that cannot lead to a valid complete solution.

### Core Principles

#### 1. Systematic Search
Backtracking explores the solution space in a depth-first manner, building solutions incrementally.

#### 2. Constraint Satisfaction
At each step, we check if the current partial solution satisfies all constraints. If not, we backtrack.

#### 3. Pruning
We eliminate branches of the search tree that cannot lead to valid solutions, reducing the search space.

### Backtracking Algorithm Template
```python
def backtrack(solution, level):
    if is_complete(solution):
        if is_valid(solution):
            process_solution(solution)
        return
    
    for candidate in get_candidates(solution, level):
        if is_promising(solution, candidate, level):
            solution[level] = candidate
            backtrack(solution, level + 1)
            # Backtrack (implicit - solution[level] will be overwritten)
```

### Key Components

#### 1. Solution Representation
How we represent partial and complete solutions (array, tree, graph, etc.)

#### 2. Constraint Checking
Functions to verify if current partial solution is valid:
- `is_promising()`: Check if partial solution can lead to valid complete solution
- `is_valid()`: Check if complete solution satisfies all constraints

#### 3. Candidate Generation
`get_candidates()`: Generate possible values for next position

#### 4. Termination Condition
`is_complete()`: Check if we have a complete solution

### Time Complexity Analysis
- **Worst Case**: O(b^d) where b is branching factor and d is depth
- **Best Case**: O(d) when solution found quickly
- **Average Case**: Depends on problem structure and pruning effectiveness

### Space Complexity
- **Space**: O(d) for recursion stack and solution storage

### When to Use Backtracking
1. **Constraint Satisfaction Problems**: N-Queens, Sudoku, Graph Coloring
2. **Combinatorial Optimization**: Finding all/optimal solutions
3. **Decision Problems**: Determining if solution exists
4. **Enumeration Problems**: Generating all valid configurations

### Backtracking vs Other Approaches

| Aspect | Backtracking | Brute Force | Dynamic Programming |
|--------|--------------|-------------|-------------------|
| **Search Strategy** | Depth-first with pruning | Exhaustive search | Optimal substructure |
| **Pruning** | Yes | No | No (but avoids recomputation) |
| **Memory Usage** | O(depth) | O(1) | O(state space) |
| **When to Use** | Constraint satisfaction | Small search spaces | Overlapping subproblems |

---

## 2. 8-Queens Problem - Complete Analysis

### Problem Definition
Place 8 queens on an 8×8 chessboard such that no two queens attack each other. Queens can attack horizontally, vertically, and diagonally.

### Constraints
1. **Row Constraint**: No two queens in same row
2. **Column Constraint**: No two queens in same column  
3. **Diagonal Constraints**: 
   - Main diagonal: No two queens on same diagonal (row - col = constant)
   - Anti-diagonal: No two queens on same anti-diagonal (row + col = constant)

### Solution Representation
Use array `queen[i] = j` meaning queen in row i is placed in column j.

### Detailed Algorithm

#### Constraint Checking Functions
```python
def is_safe(board, row, col, n):
    # Check column constraint
    for i in range(row):
        if board[i] == col:
            return False
    
    # Check main diagonal (row - col = constant)
    for i in range(row):
        if board[i] - i == col - row:
            return False
    
    # Check anti-diagonal (row + col = constant)  
    for i in range(row):
        if board[i] + i == col + row:
            return False
    
    return True

def solve_n_queens(n):
    board = [-1] * n
    solutions = []
    
    def backtrack(row):
        if row == n:
            solutions.append(board[:])  # Found a solution
            return
        
        for col in range(n):
            if is_safe(board, row, col, n):
                board[row] = col
                backtrack(row + 1)
                # Implicit backtrack - board[row] will be overwritten
    
    backtrack(0)
    return solutions
```

### Step-by-Step Solution for 8-Queens

#### Manual Solution Process
Let's trace through finding one solution:

**Row 0**: Try column 0
- Place queen at (0,0)
- Check constraints: All satisfied for first queen

**Row 1**: Try columns 0,1,2,3...
- Column 0: Conflicts with queen at (0,0) - same column
- Column 1: Conflicts with queen at (0,0) - diagonal
- Column 2: Safe! Place queen at (1,2)

**Row 2**: Try columns 0,1,2,3,4...
- Column 0: Conflicts with (0,0) - same column
- Column 1: Conflicts with (1,2) - diagonal  
- Column 2: Conflicts with (1,2) - same column
- Column 3: Conflicts with (1,2) - diagonal
- Column 4: Safe! Place queen at (2,4)

**Continue this process...**

#### One Valid Solution
```
Solution: [0, 4, 7, 5, 2, 6, 1, 3]
Board representation:
Q . . . . . . .  (Row 0, Col 0)
. . . . Q . . .  (Row 1, Col 4)  
. . . . . . . Q  (Row 2, Col 7)
. . . . . Q . .  (Row 3, Col 5)
. . Q . . . . .  (Row 4, Col 2)
. . . . . . Q .  (Row 5, Col 6)
. Q . . . . . .  (Row 6, Col 1)
. . . Q . . . .  (Row 7, Col 3)
```

### Optimized Implementation
```python
class NQueens:
    def __init__(self, n):
        self.n = n
        self.board = [-1] * n
        self.solutions = []
        
        # Optimization: Use sets for O(1) constraint checking
        self.cols = set()
        self.main_diag = set()  # row - col
        self.anti_diag = set()  # row + col
    
    def is_safe_optimized(self, row, col):
        return (col not in self.cols and 
                (row - col) not in self.main_diag and
                (row + col) not in self.anti_diag)
    
    def place_queen(self, row, col):
        self.board[row] = col
        self.cols.add(col)
        self.main_diag.add(row - col)
        self.anti_diag.add(row + col)
    
    def remove_queen(self, row, col):
        self.board[row] = -1
        self.cols.remove(col)
        self.main_diag.remove(row - col)
        self.anti_diag.remove(row + col)
    
    def solve(self):
        def backtrack(row):
            if row == self.n:
                self.solutions.append(self.board[:])
                return
            
            for col in range(self.n):
                if self.is_safe_optimized(row, col):
                    self.place_queen(row, col)
                    backtrack(row + 1)
                    self.remove_queen(row, col)
        
        backtrack(0)
        return self.solutions
```

### Analysis of 8-Queens

#### Number of Solutions
- **8-Queens**: 92 distinct solutions
- **4-Queens**: 2 distinct solutions
- **General N-Queens**: Varies exponentially with N

#### Time Complexity
- **Worst Case**: O(N!) - try all permutations
- **With Pruning**: Much better in practice due to constraint checking
- **Optimized Version**: O(1) constraint checking vs O(N) in naive version

#### Space Complexity
- **Recursion Stack**: O(N)
- **Additional Storage**: O(N) for constraint sets

### Variations and Extensions

#### 1. Count Solutions Only
```python
def count_n_queens(n):
    count = 0
    board = [-1] * n
    
    def backtrack(row):
        nonlocal count
        if row == n:
            count += 1
            return
        
        for col in range(n):
            if is_safe(board, row, col, n):
                board[row] = col
                backtrack(row + 1)
    
    backtrack(0)
    return count
```

#### 2. Find First Solution Only
```python
def find_first_solution(n):
    board = [-1] * n
    
    def backtrack(row):
        if row == n:
            return True  # Found solution
        
        for col in range(n):
            if is_safe(board, row, col, n):
                board[row] = col
                if backtrack(row + 1):
                    return True
        
        return False  # No solution found
    
    if backtrack(0):
        return board
    return None
```

#### 3. Symmetric Solutions
Many solutions are rotations/reflections of others. Can reduce search space by considering symmetries.

### Applications Beyond Chess
1. **VLSI Design**: Component placement
2. **Scheduling**: Resource allocation
3. **Cryptography**: Key generation
4. **Combinatorial Design**: Experimental design
---

##
 3. Hamiltonian Cycle Problem - Detailed Analysis

### Problem Definition
A Hamiltonian cycle is a cycle that visits every vertex in a graph exactly once and returns to the starting vertex. The Hamiltonian Cycle Problem asks whether such a cycle exists in a given graph.

### Problem Characteristics
- **Input**: Undirected or directed graph G = (V, E)
- **Output**: Hamiltonian cycle if exists, or "No cycle exists"
- **Complexity**: NP-Complete problem
- **Applications**: Traveling salesman, circuit design, DNA sequencing

### Mathematical Formulation
Given graph G = (V, E) with n vertices:
- Find sequence of vertices v₁, v₂, ..., vₙ, v₁ such that:
  1. Each vertex appears exactly once (except start/end)
  2. (vᵢ, vᵢ₊₁) ∈ E for all i = 1 to n-1
  3. (vₙ, v₁) ∈ E

### Backtracking Algorithm for Hamiltonian Cycle

#### Algorithm Structure
```python
def hamiltonian_cycle(graph, n):
    path = [-1] * n
    path[0] = 0  # Start from vertex 0
    
    def is_safe(vertex, pos):
        # Check if vertex is adjacent to previous vertex in path
        if graph[path[pos-1]][vertex] == 0:
            return False
        
        # Check if vertex is already in path
        if vertex in path[:pos]:
            return False
        
        return True
    
    def solve_hamiltonian(pos):
        # Base case: if all vertices are included
        if pos == n:
            # Check if there's edge from last vertex to first
            return graph[path[pos-1]][path[0]] == 1
        
        # Try different vertices as next candidate
        for vertex in range(1, n):  # Skip vertex 0 as it's already in path
            if is_safe(vertex, pos):
                path[pos] = vertex
                
                if solve_hamiltonian(pos + 1):
                    return True
                
                # Backtrack
                path[pos] = -1
        
        return False
    
    if solve_hamiltonian(1):
        return path
    return None
```

### Complete Example: Finding Hamiltonian Cycle

#### Example Graph
```
Graph with 5 vertices (0,1,2,3,4):
Adjacency Matrix:
    0  1  2  3  4
0 [ 0  1  0  1  0 ]
1 [ 1  0  1  1  1 ]  
2 [ 0  1  0  0  1 ]
3 [ 1  1  0  0  1 ]
4 [ 0  1  1  1  0 ]

Visual representation:
    0 ---- 1 ---- 2
    |      |      |
    |      |      |
    3 ---- 4 ------
```

#### Step-by-Step Solution Process

**Initial State**: path = [0, -1, -1, -1, -1], pos = 1

**Step 1**: Try vertex 1 at position 1
- is_safe(1, 1): Check if (0,1) edge exists → Yes
- Check if 1 already in path → No
- path = [0, 1, -1, -1, -1], move to pos = 2

**Step 2**: Try vertex 2 at position 2  
- is_safe(2, 2): Check if (1,2) edge exists → Yes
- Check if 2 already in path → No
- path = [0, 1, 2, -1, -1], move to pos = 3

**Step 3**: Try vertex 3 at position 3
- is_safe(3, 3): Check if (2,3) edge exists → No
- Try vertex 4: Check if (2,4) edge exists → Yes
- path = [0, 1, 2, 4, -1], move to pos = 4

**Step 4**: Try vertex 3 at position 4
- is_safe(3, 4): Check if (4,3) edge exists → Yes
- Check if 3 already in path → No
- path = [0, 1, 2, 4, 3], move to pos = 5

**Step 5**: Check cycle completion (pos = n = 5)
- Check if edge (3,0) exists → Yes
- **Hamiltonian Cycle Found**: 0 → 1 → 2 → 4 → 3 → 0

### Advanced Implementation with Optimizations

```python
class HamiltonianCycle:
    def __init__(self, graph):
        self.graph = graph
        self.n = len(graph)
        self.path = []
        
    def is_valid_edge(self, u, v):
        return self.graph[u][v] == 1
    
    def find_all_cycles(self):
        all_cycles = []
        path = [0]  # Start from vertex 0
        visited = [False] * self.n
        visited[0] = True
        
        def backtrack(current_vertex, path_length):
            if path_length == self.n:
                # Check if we can return to start
                if self.is_valid_edge(path[-1], path[0]):
                    all_cycles.append(path[:] + [path[0]])
                return
            
            for next_vertex in range(self.n):
                if (not visited[next_vertex] and 
                    self.is_valid_edge(current_vertex, next_vertex)):
                    
                    visited[next_vertex] = True
                    path.append(next_vertex)
                    
                    backtrack(next_vertex, path_length + 1)
                    
                    # Backtrack
                    visited[next_vertex] = False
                    path.pop()
        
        backtrack(0, 1)
        return all_cycles
    
    def has_hamiltonian_cycle(self):
        """Check if Hamiltonian cycle exists (faster than finding all)"""
        path = [0]
        visited = [False] * self.n
        visited[0] = True
        
        def exists_cycle(current_vertex, path_length):
            if path_length == self.n:
                return self.is_valid_edge(path[-1], path[0])
            
            for next_vertex in range(self.n):
                if (not visited[next_vertex] and 
                    self.is_valid_edge(current_vertex, next_vertex)):
                    
                    visited[next_vertex] = True
                    path.append(next_vertex)
                    
                    if exists_cycle(next_vertex, path_length + 1):
                        return True
                    
                    visited[next_vertex] = False
                    path.pop()
            
            return False
        
        return exists_cycle(0, 1)
```

### Hamiltonian Path vs Hamiltonian Cycle

#### Hamiltonian Path
- Visits every vertex exactly once
- Does not need to return to starting vertex
- Slightly easier problem but still NP-Complete

```python
def hamiltonian_path(graph, start_vertex):
    n = len(graph)
    path = [start_vertex]
    visited = [False] * n
    visited[start_vertex] = True
    
    def find_path(current_vertex, path_length):
        if path_length == n:
            return True
        
        for next_vertex in range(n):
            if (not visited[next_vertex] and 
                graph[current_vertex][next_vertex] == 1):
                
                visited[next_vertex] = True
                path.append(next_vertex)
                
                if find_path(next_vertex, path_length + 1):
                    return True
                
                visited[next_vertex] = False
                path.pop()
        
        return False
    
    if find_path(start_vertex, 1):
        return path
    return None
```

### Time and Space Complexity

#### Time Complexity
- **Worst Case**: O(N!) - try all permutations of vertices
- **With Pruning**: Better in practice, but still exponential
- **Best Case**: O(N) if cycle found quickly

#### Space Complexity
- **Recursion Stack**: O(N)
- **Path Storage**: O(N)
- **Visited Array**: O(N)
- **Total**: O(N)

### Optimization Techniques

#### 1. Degree-Based Pruning
```python
def degree_pruning(graph):
    n = len(graph)
    degrees = [sum(row) for row in graph]
    
    # If any vertex has degree < 2, no Hamiltonian cycle possible
    if any(degree < 2 for degree in degrees):
        return False
    return True
```

#### 2. Dirac's Theorem
If every vertex has degree ≥ n/2, then Hamiltonian cycle exists.

#### 3. Ore's Theorem  
If for every pair of non-adjacent vertices u,v: degree(u) + degree(v) ≥ n, then Hamiltonian cycle exists.

### Applications

#### 1. Traveling Salesman Problem
- Find shortest Hamiltonian cycle
- Add edge weights and optimize for minimum cost

#### 2. Knight's Tour
- Knight visits every square on chessboard exactly once
- Special case of Hamiltonian path on knight's graph

#### 3. DNA Sequencing
- Reconstruct DNA sequence from fragments
- Model as Hamiltonian path problem

#### 4. Circuit Design
- Design circuits that visit all components
- Minimize wire length and complexity

---

## 4. Graph Coloring Problem - Detailed Analysis

### Problem Definition
Graph coloring assigns colors to vertices of a graph such that no two adjacent vertices have the same color. The goal is to find the minimum number of colors needed (chromatic number).

### Types of Graph Coloring

#### 1. Vertex Coloring
Color vertices such that adjacent vertices have different colors.

#### 2. Edge Coloring  
Color edges such that adjacent edges have different colors.

#### 3. Face Coloring
Color faces of planar graph such that adjacent faces have different colors.

### Mathematical Formulation
Given graph G = (V, E):
- Find coloring function f: V → {1, 2, ..., k}
- Such that f(u) ≠ f(v) for all (u,v) ∈ E
- Minimize k (chromatic number χ(G))

### Backtracking Algorithm for Graph Coloring

#### Basic Algorithm Structure
```python
def graph_coloring(graph, num_colors):
    n = len(graph)
    colors = [0] * n  # 0 means uncolored
    
    def is_safe(vertex, color):
        # Check if assigning color to vertex is safe
        for neighbor in range(n):
            if graph[vertex][neighbor] == 1 and colors[neighbor] == color:
                return False
        return True
    
    def solve_coloring(vertex):
        # Base case: all vertices colored
        if vertex == n:
            return True
        
        # Try all colors for current vertex
        for color in range(1, num_colors + 1):
            if is_safe(vertex, color):
                colors[vertex] = color
                
                if solve_coloring(vertex + 1):
                    return True
                
                # Backtrack
                colors[vertex] = 0
        
        return False
    
    if solve_coloring(0):
        return colors
    return None
```

### Complete Example from June 2024 Exam

#### Given Graph (from exam question)
```
Undirected Graph with 6 vertices: a, b, c, d, e, f
Edges: (a,b), (b,f), (f,e), (e,a), (a,c), (b,c), (c,d), (d,e), (d,f)

Visual representation:
    a ---- b
    |\     |\
    | \    | \
    |  c---d  f
    |  |   | /
    |  |   |/
    e ------
```

#### Step-by-Step Coloring Process

**Adjacency Matrix**:
```
   a b c d e f
a [0 1 1 0 1 0]
b [1 0 1 0 0 1]  
c [1 1 0 1 0 0]
d [0 0 1 0 1 1]
e [1 0 0 1 0 0]
f [0 1 0 1 0 0]
```

**Coloring Process** (using colors 1, 2, 3):

**Vertex a (index 0)**: Try color 1
- No neighbors colored yet → Safe
- colors = [1, 0, 0, 0, 0, 0]

**Vertex b (index 1)**: Try color 1
- Adjacent to a (color 1) → Not safe
- Try color 2 → Safe
- colors = [1, 2, 0, 0, 0, 0]

**Vertex c (index 2)**: Try color 1
- Adjacent to a (color 1) → Not safe
- Try color 2 → Adjacent to b (color 2) → Not safe
- Try color 3 → Safe
- colors = [1, 2, 3, 0, 0, 0]

**Vertex d (index 3)**: Try color 1
- Adjacent to c (color 3), not adjacent to any vertex with color 1 → Safe
- colors = [1, 2, 3, 1, 0, 0]

**Vertex e (index 4)**: Try color 1
- Adjacent to a (color 1) and d (color 1) → Not safe
- Try color 2 → Safe (not adjacent to any vertex with color 2)
- colors = [1, 2, 3, 1, 2, 0]

**Vertex f (index 5)**: Try color 1
- Adjacent to b (color 2) and d (color 1) → Not safe for color 1
- Try color 2 → Adjacent to b (color 2) → Not safe
- Try color 3 → Safe
- colors = [1, 2, 3, 1, 2, 3]

**Final Coloring**:
- a: Color 1 (Red)
- b: Color 2 (Blue)  
- c: Color 3 (Green)
- d: Color 1 (Red)
- e: Color 2 (Blue)
- f: Color 3 (Green)

**Chromatic Number**: 3 (minimum colors needed)

### Advanced Graph Coloring Implementation

```python
class GraphColoring:
    def __init__(self, graph):
        self.graph = graph
        self.n = len(graph)
        self.chromatic_number = None
    
    def is_safe_to_color(self, vertex, color, coloring):
        for neighbor in range(self.n):
            if (self.graph[vertex][neighbor] == 1 and 
                coloring[neighbor] == color):
                return False
        return True
    
    def find_chromatic_number(self):
        """Find minimum number of colors needed"""
        for num_colors in range(1, self.n + 1):
            if self.can_color_with_k_colors(num_colors):
                self.chromatic_number = num_colors
                return num_colors
        return self.n  # Worst case: n colors
    
    def can_color_with_k_colors(self, k):
        coloring = [0] * self.n
        
        def backtrack(vertex):
            if vertex == self.n:
                return True
            
            for color in range(1, k + 1):
                if self.is_safe_to_color(vertex, color, coloring):
                    coloring[vertex] = color
                    
                    if backtrack(vertex + 1):
                        return True
                    
                    coloring[vertex] = 0
            
            return False
        
        return backtrack(0)
    
    def find_all_colorings(self, num_colors):
        """Find all possible colorings with given number of colors"""
        all_colorings = []
        coloring = [0] * self.n
        
        def backtrack(vertex):
            if vertex == self.n:
                all_colorings.append(coloring[:])
                return
            
            for color in range(1, num_colors + 1):
                if self.is_safe_to_color(vertex, color, coloring):
                    coloring[vertex] = color
                    backtrack(vertex + 1)
                    coloring[vertex] = 0
        
        backtrack(0)
        return all_colorings
    
    def greedy_coloring(self):
        """Greedy approximation algorithm"""
        coloring = [0] * self.n
        
        for vertex in range(self.n):
            # Find available colors
            used_colors = set()
            for neighbor in range(self.n):
                if (self.graph[vertex][neighbor] == 1 and 
                    coloring[neighbor] != 0):
                    used_colors.add(coloring[neighbor])
            
            # Assign smallest available color
            color = 1
            while color in used_colors:
                color += 1
            coloring[vertex] = color
        
        return coloring, max(coloring)
```

### Graph Coloring Theorems and Properties

#### 1. Four Color Theorem
Every planar graph can be colored with at most 4 colors.

#### 2. Brooks' Theorem
For connected graph G (not complete or odd cycle):
χ(G) ≤ Δ(G) where Δ(G) is maximum degree.

#### 3. Chromatic Polynomial
P(G, k) = number of proper colorings of G with k colors.

#### 4. Bounds on Chromatic Number
- **Lower Bound**: χ(G) ≥ ω(G) (clique number)
- **Upper Bound**: χ(G) ≤ Δ(G) + 1 (maximum degree + 1)

### Special Cases and Optimizations

#### 1. Bipartite Graphs
```python
def is_bipartite_and_color(graph):
    n = len(graph)
    colors = [-1] * n
    
    def bfs_color(start):
        queue = [start]
        colors[start] = 0
        
        while queue:
            vertex = queue.pop(0)
            
            for neighbor in range(n):
                if graph[vertex][neighbor] == 1:
                    if colors[neighbor] == -1:
                        colors[neighbor] = 1 - colors[vertex]
                        queue.append(neighbor)
                    elif colors[neighbor] == colors[vertex]:
                        return False
        return True
    
    # Check all components
    for vertex in range(n):
        if colors[vertex] == -1:
            if not bfs_color(vertex):
                return False, None
    
    return True, colors
```

#### 2. Perfect Graphs
For perfect graphs: χ(G) = ω(G) for all induced subgraphs.

### Time and Space Complexity

#### Backtracking Approach
- **Time Complexity**: O(k^n) where k is number of colors, n is vertices
- **Space Complexity**: O(n) for recursion stack and coloring array

#### Greedy Approach
- **Time Complexity**: O(n²) for adjacency matrix representation
- **Space Complexity**: O(n)
- **Approximation Ratio**: At most Δ(G) + 1 colors

### Applications of Graph Coloring

#### 1. Scheduling Problems
- **Course Scheduling**: Courses are vertices, conflicts are edges
- **Exam Scheduling**: Minimize time slots needed
- **Resource Allocation**: Assign resources avoiding conflicts

#### 2. Register Allocation
- **Compiler Design**: Variables are vertices, interference is edges
- **Minimize Registers**: Each color represents a register

#### 3. Frequency Assignment
- **Radio Networks**: Stations are vertices, interference is edges
- **Minimize Frequencies**: Each color represents a frequency

#### 4. Map Coloring
- **Geographic Maps**: Regions are vertices, borders are edges
- **Minimize Colors**: Each color represents a different color on map

### Variations of Graph Coloring

#### 1. List Coloring
Each vertex has a list of allowed colors.

#### 2. Equitable Coloring
Color classes differ in size by at most 1.

#### 3. Acyclic Coloring
No two adjacent vertices have same color, and no bichromatic cycles exist.

#### 4. Total Coloring
Color both vertices and edges such that no two adjacent/incident elements have same color.---


## 5. Introduction to Branch & Bound Method - Detailed Analysis

### What is Branch & Bound?
Branch & Bound is a systematic enumeration technique for solving optimization problems. It explores the solution space by branching (dividing problems into subproblems) and bounding (eliminating subproblems that cannot lead to optimal solutions).

### Core Concepts

#### 1. Branching
- **Divide**: Split the problem into smaller subproblems
- **Conquer**: Solve subproblems recursively
- **Search Tree**: Each node represents a subproblem

#### 2. Bounding
- **Lower Bound**: Minimum possible value for minimization problems
- **Upper Bound**: Maximum possible value for maximization problems
- **Pruning**: Eliminate branches that cannot improve current best solution

#### 3. Best-First Search
- **Priority Queue**: Explore most promising nodes first
- **Heuristic**: Use bounds to guide search
- **Efficiency**: Avoid exploring unpromising branches

### Branch & Bound Algorithm Template

```python
import heapq
from dataclasses import dataclass
from typing import Any, List, Optional

@dataclass
class Node:
    level: int
    bound: float
    solution: List[Any]
    cost: float = 0
    
    def __lt__(self, other):
        return self.bound < other.bound  # For min-heap

def branch_and_bound_template(problem):
    # Initialize
    best_solution = None
    best_cost = float('inf')  # For minimization
    
    # Priority queue for nodes to explore
    pq = []
    
    # Create root node
    root = create_root_node(problem)
    heapq.heappush(pq, root)
    
    while pq:
        current_node = heapq.heappop(pq)
        
        # Pruning: if bound is worse than best known solution
        if current_node.bound >= best_cost:
            continue
        
        # Check if complete solution
        if is_complete_solution(current_node):
            if current_node.cost < best_cost:
                best_cost = current_node.cost
                best_solution = current_node.solution
        else:
            # Branch: generate child nodes
            children = generate_children(current_node, problem)
            
            for child in children:
                child.bound = calculate_bound(child, problem)
                
                # Only add promising children
                if child.bound < best_cost:
                    heapq.heappush(pq, child)
    
    return best_solution, best_cost
```

### Key Components

#### 1. Node Representation
```python
class BBNode:
    def __init__(self, level=0, cost=0, bound=0, solution=None):
        self.level = level      # Depth in search tree
        self.cost = cost        # Cost of current partial solution
        self.bound = bound      # Lower/upper bound estimate
        self.solution = solution or []  # Partial solution
        self.included = []      # Items included so far
        self.excluded = []      # Items excluded so far
```

#### 2. Bounding Function
The quality of bounds determines efficiency:
- **Tight Bounds**: Better pruning, fewer nodes explored
- **Loose Bounds**: Poor pruning, more nodes explored
- **Computation Cost**: Balance between bound quality and computation time

#### 3. Branching Strategy
- **Binary Branching**: Include/exclude decisions
- **Multi-way Branching**: Multiple choices at each node
- **Variable Ordering**: Choose variables to branch on

### Branch & Bound vs Other Methods

| Aspect | Branch & Bound | Backtracking | Dynamic Programming |
|--------|----------------|--------------|-------------------|
| **Approach** | Best-first search | Depth-first search | Bottom-up/Top-down |
| **Pruning** | Bound-based | Constraint-based | None (but avoids recomputation) |
| **Optimality** | Guaranteed optimal | May find any valid solution | Guaranteed optimal |
| **Memory** | Can be high (queue) | Low (stack) | High (table) |
| **Best For** | Optimization problems | Feasibility problems | Overlapping subproblems |

### When to Use Branch & Bound
1. **Optimization Problems**: Need optimal solution, not just feasible
2. **NP-Hard Problems**: When exact solution needed despite complexity
3. **Good Bounds Available**: Can compute tight bounds efficiently
4. **Moderate Problem Size**: Exponential worst-case but practical for many instances

---

## 6. Traveling Salesman Problem using Branch & Bound - Complete Analysis

### Problem Definition
Given a set of cities and distances between them, find the shortest possible route that visits each city exactly once and returns to the starting city.

### Mathematical Formulation
- **Input**: Distance matrix D[i][j] = distance from city i to city j
- **Output**: Permutation π of cities minimizing total distance
- **Objective**: Minimize Σ D[π(i)][π(i+1)] + D[π(n)][π(1)]

### TSP Branch & Bound Algorithm

#### Node Representation for TSP
```python
class TSPNode:
    def __init__(self):
        self.level = 0          # Number of cities included in path
        self.path = []          # Current path
        self.cost = 0           # Cost of current path
        self.bound = 0          # Lower bound estimate
        self.visited = set()    # Set of visited cities
        self.reduced_matrix = None  # Reduced cost matrix
```

#### Lower Bound Calculation
The key to efficient TSP branch & bound is computing tight lower bounds using matrix reduction:

```python
def calculate_lower_bound(matrix, path, visited, n):
    """Calculate lower bound using row and column reduction"""
    
    # Create reduced matrix
    reduced = [row[:] for row in matrix]
    bound = 0
    
    # Step 1: Row reduction
    for i in range(n):
        if i not in visited or (len(path) > 0 and i == path[-1]):
            row_min = min(reduced[i][j] for j in range(n) 
                         if j not in visited or (len(path) == 0 and j == 0))
            if row_min != float('inf'):
                bound += row_min
                for j in range(n):
                    if reduced[i][j] != float('inf'):
                        reduced[i][j] -= row_min
    
    # Step 2: Column reduction  
    for j in range(n):
        if j not in visited or (len(path) == 0 and j == 0):
            col_min = min(reduced[i][j] for i in range(n) 
                         if i not in visited or (len(path) > 0 and i == path[-1]))
            if col_min != float('inf'):
                bound += col_min
                for i in range(n):
                    if reduced[i][j] != float('inf'):
                        reduced[i][j] -= col_min
    
    return bound, reduced
```

#### Complete TSP Branch & Bound Implementation

```python
import heapq
from copy import deepcopy

class TSPBranchBound:
    def __init__(self, distance_matrix):
        self.matrix = distance_matrix
        self.n = len(distance_matrix)
        self.best_cost = float('inf')
        self.best_path = None
        self.nodes_explored = 0
    
    def solve(self):
        # Priority queue for nodes (min-heap based on bound)
        pq = []
        
        # Create root node
        root = TSPNode()
        root.level = 0
        root.path = [0]  # Start from city 0
        root.visited = {0}
        root.cost = 0
        root.bound, root.reduced_matrix = self.calculate_initial_bound()
        
        heapq.heappush(pq, (root.bound, 0, root))  # (bound, tie_breaker, node)
        tie_breaker = 1
        
        while pq:
            _, _, current = heapq.heappop(pq)
            self.nodes_explored += 1
            
            # Pruning: if bound >= best known cost
            if current.bound >= self.best_cost:
                continue
            
            # If all cities visited
            if current.level == self.n - 1:
                # Add cost to return to start
                total_cost = current.cost + self.matrix[current.path[-1]][0]
                if total_cost < self.best_cost:
                    self.best_cost = total_cost
                    self.best_path = current.path + [0]
            else:
                # Branch: try all unvisited cities
                for next_city in range(self.n):
                    if next_city not in current.visited:
                        child = self.create_child_node(current, next_city)
                        
                        if child.bound < self.best_cost:
                            heapq.heappush(pq, (child.bound, tie_breaker, child))
                            tie_breaker += 1
        
        return self.best_path, self.best_cost
    
    def calculate_initial_bound(self):
        """Calculate initial lower bound using matrix reduction"""
        reduced = [row[:] for row in self.matrix]
        bound = 0
        
        # Row reduction
        for i in range(self.n):
            row_min = min(reduced[i])
            if row_min != float('inf'):
                bound += row_min
                for j in range(self.n):
                    reduced[i][j] -= row_min
        
        # Column reduction
        for j in range(self.n):
            col_min = min(reduced[i][j] for i in range(self.n))
            if col_min != float('inf'):
                bound += col_min
                for i in range(self.n):
                    reduced[i][j] -= col_min
        
        return bound, reduced
    
    def create_child_node(self, parent, next_city):
        """Create child node by adding next_city to path"""
        child = TSPNode()
        child.level = parent.level + 1
        child.path = parent.path + [next_city]
        child.visited = parent.visited | {next_city}
        child.cost = parent.cost + self.matrix[parent.path[-1]][next_city]
        
        # Calculate bound for child
        child.bound = self.calculate_child_bound(parent, next_city)
        
        return child
    
    def calculate_child_bound(self, parent, next_city):
        """Calculate bound for child node"""
        current_city = parent.path[-1]
        
        # Start with parent's bound
        bound = parent.bound
        
        # Subtract the minimum values that are no longer achievable
        # This is a simplified bound calculation
        # In practice, you'd use more sophisticated reduction
        
        return bound + self.matrix[current_city][next_city]
```

### Complete Example: TSP with Branch & Bound

#### Example Problem
```
4 cities with distance matrix:
    0   1   2   3
0 [ ∞  10  15  20 ]
1 [ 10  ∞  35  25 ]
2 [ 15  35  ∞  30 ]
3 [ 20  25  30  ∞ ]
```

#### Step-by-Step Solution

**Step 1: Initial Bound Calculation**
```
Original Matrix:
    0   1   2   3
0 [ ∞  10  15  20 ]
1 [ 10  ∞  35  25 ]
2 [ 15  35  ∞  30 ]
3 [ 20  25  30  ∞ ]

Row Reduction:
Row 0: min = 10, subtract 10: [ ∞   0   5  10 ]
Row 1: min = 10, subtract 10: [  0  ∞  25  15 ]
Row 2: min = 15, subtract 15: [  0  20  ∞  15 ]
Row 3: min = 20, subtract 20: [  0   5  10  ∞ ]

After Row Reduction:
    0   1   2   3
0 [ ∞   0   5  10 ]
1 [  0  ∞  25  15 ]
2 [  0  20  ∞  15 ]
3 [  0   5  10  ∞ ]

Column Reduction:
Col 0: min = 0, no change
Col 1: min = 0, no change  
Col 2: min = 5, subtract 5: [ 0, 20, ∞, 5 ]
Col 3: min = 10, subtract 10: [ 0, 5, 5, ∞ ]

Final Reduced Matrix:
    0   1   2   3
0 [ ∞   0   0   0 ]
1 [  0  ∞  20   5 ]
2 [  0  20  ∞   5 ]
3 [  0   5   5  ∞ ]

Initial Lower Bound = 10 + 10 + 15 + 20 + 5 + 10 = 70
```

**Step 2: Branching from Root**
Root node: path = [0], bound = 70

Branch to cities 1, 2, 3:

**Node (0→1)**: 
- Cost = 10
- Bound calculation (simplified) ≈ 70
- Add to queue

**Node (0→2)**:
- Cost = 15  
- Bound calculation ≈ 75
- Add to queue

**Node (0→3)**:
- Cost = 20
- Bound calculation ≈ 80
- Add to queue

**Step 3: Continue Branching**
Process node with best bound (0→1):

From (0→1), branch to cities 2, 3:
- (0→1→2): Cost = 10 + 35 = 45, bound ≈ 85
- (0→1→3): Cost = 10 + 25 = 35, bound ≈ 75

**Step 4: Complete Solutions**
Eventually find complete tours:
- 0→1→3→2→0: Cost = 10 + 25 + 30 + 15 = 80
- 0→2→3→1→0: Cost = 15 + 30 + 25 + 10 = 80  
- 0→3→1→2→0: Cost = 20 + 25 + 35 + 15 = 95

**Optimal Solution**: 0→1→3→2→0 or 0→2→3→1→0 with cost 80

### Advanced TSP Optimizations

#### 1. Held-Karp Lower Bound
```python
def held_karp_bound(matrix, subset, last):
    """More sophisticated lower bound using Held-Karp relaxation"""
    n = len(matrix)
    
    # Minimum spanning tree on remaining vertices
    remaining = set(range(n)) - subset
    if len(remaining) <= 1:
        return 0
    
    # Calculate MST cost (simplified)
    mst_cost = 0
    # ... MST calculation code ...
    
    return mst_cost
```

#### 2. Christofides Heuristic for Upper Bound
```python
def christofides_upper_bound(matrix):
    """Get good upper bound using Christofides algorithm"""
    # 1. Find MST
    # 2. Find minimum weight perfect matching on odd-degree vertices
    # 3. Combine to get Eulerian graph
    # 4. Find Eulerian tour
    # 5. Convert to Hamiltonian tour
    pass
```

#### 3. Cutting Planes
Add additional constraints to tighten bounds:
- Subtour elimination constraints
- Comb inequalities
- Clique tree inequalities

### Time and Space Complexity

#### Time Complexity
- **Worst Case**: O(n! × n²) - explore all permutations
- **Best Case**: O(n³) - with very tight bounds
- **Average Case**: Depends on bound quality and problem structure

#### Space Complexity
- **Priority Queue**: O(b^d) where b is branching factor, d is depth
- **Node Storage**: O(n) per node
- **Total**: Can be exponential in worst case

### TSP Variants

#### 1. Asymmetric TSP (ATSP)
Distance from i to j ≠ distance from j to i

#### 2. TSP with Time Windows
Each city must be visited within specific time window

#### 3. Multiple TSP (mTSP)
Multiple salesmen, each starting from depot

#### 4. TSP with Pickup and Delivery
Items must be picked up before delivery

### Applications of TSP
1. **Logistics**: Vehicle routing, delivery optimization
2. **Manufacturing**: Drill path optimization, PCB manufacturing
3. **Bioinformatics**: DNA sequencing, protein folding
4. **VLSI Design**: Wire routing, component placement---


## 7. Lower Bound Theory - Detailed Analysis

### What is Lower Bound Theory?
Lower bound theory establishes the minimum amount of resources (time, space, comparisons, etc.) required to solve a problem in the worst case. It provides theoretical limits on algorithm efficiency.

### Types of Lower Bounds

#### 1. Information-Theoretic Lower Bounds
Based on the amount of information needed to solve the problem.

**Example: Sorting**
- Need to distinguish between n! possible orderings
- Requires at least ⌈log₂(n!)⌉ bits of information
- Using Stirling's approximation: log₂(n!) ≈ n log₂(n) - n log₂(e)
- **Lower bound for comparison-based sorting**: Ω(n log n)

#### 2. Adversary Lower Bounds
Construct an adversary that forces any algorithm to do a certain amount of work.

**Example: Finding Maximum**
```python
def adversary_max_lower_bound():
    """
    Adversary argument for finding maximum of n elements:
    - Initially, no element is known to be non-maximum
    - Each comparison eliminates at most one element from being maximum
    - Need at least n-1 comparisons to eliminate n-1 elements
    """
    return "Lower bound: n-1 comparisons"
```

#### 3. Algebraic Lower Bounds
Based on algebraic properties and decision trees.

**Example: Element Distinctness**
- Problem: Determine if all elements in array are distinct
- **Lower bound**: Ω(n log n) in algebraic decision tree model

#### 4. Communication Complexity Lower Bounds
For distributed algorithms, based on communication requirements.

### Lower Bound Techniques

#### 1. Counting Arguments
```python
def counting_argument_example():
    """
    Example: Lower bound for sorting n distinct elements
    
    - There are n! possible permutations
    - Each comparison has 2 outcomes
    - Need at least log₂(n!) comparisons
    - log₂(n!) = Ω(n log n)
    """
    import math
    
    def stirling_approximation(n):
        return n * math.log2(n) - n * math.log2(math.e)
    
    return stirling_approximation
```

#### 2. Reduction Arguments
```python
def reduction_lower_bound():
    """
    If problem A reduces to problem B, then:
    Lower bound of A ≤ Lower bound of B
    
    Example: Element Distinctness reduces to Sorting
    - If we can sort in o(n log n), we can solve distinctness in o(n log n)
    - But distinctness has Ω(n log n) lower bound
    - Therefore, sorting has Ω(n log n) lower bound
    """
    pass
```

#### 3. Decision Tree Model
```python
class DecisionTree:
    """Model computation as binary decision tree"""
    
    def __init__(self):
        self.comparisons = 0
        self.leaves = 0
    
    def lower_bound_height(self, num_outcomes):
        """
        Decision tree with L leaves has height ≥ log₂(L)
        For sorting: L = n!, so height ≥ log₂(n!) = Ω(n log n)
        """
        import math
        return math.ceil(math.log2(num_outcomes))
```

### Lower Bounds for Specific Problems

#### 1. Sorting Lower Bound
```python
def sorting_lower_bound_proof():
    """
    Theorem: Any comparison-based sorting algorithm requires 
    Ω(n log n) comparisons in the worst case.
    
    Proof:
    1. There are n! possible permutations of n elements
    2. Each comparison has 2 outcomes (≤ or >)
    3. Decision tree has n! leaves (one for each permutation)
    4. Binary tree with n! leaves has height ≥ log₂(n!)
    5. log₂(n!) = Ω(n log n) by Stirling's approximation
    """
    
    import math
    
    def factorial_log(n):
        return sum(math.log2(i) for i in range(1, n + 1))
    
    def stirling_bound(n):
        return n * math.log2(n) - n * math.log2(math.e)
    
    # Demonstrate the bound
    for n in [10, 100, 1000]:
        exact = factorial_log(n)
        approx = stirling_bound(n)
        print(f"n={n}: log₂(n!)={exact:.2f}, Stirling≈{approx:.2f}")
```

#### 2. Selection Lower Bound
```python
def selection_lower_bound():
    """
    Finding k-th smallest element:
    - Lower bound: Ω(n) for any fixed k
    - Proof: Must examine all elements (adversary argument)
    
    Finding median (k = n/2):
    - Lower bound: Ω(n)
    - Optimal algorithm exists (median-of-medians)
    """
    
    def adversary_selection(n, k):
        """
        Adversary forces algorithm to examine all n elements
        by keeping k-th element unknown until the end
        """
        return n  # Must examine all elements
```

#### 3. Matrix Multiplication Lower Bound
```python
def matrix_multiplication_bounds():
    """
    Current best upper bound: O(n^2.373) (Coppersmith-Winograd)
    Lower bound: Ω(n²) (must read all input)
    
    Open problem: Is matrix multiplication in O(n²⁺ᵋ) for any ε > 0?
    """
    
    def naive_bound():
        return "O(n³)"
    
    def strassen_bound():
        return "O(n^2.807)"
    
    def current_best():
        return "O(n^2.373)"
    
    def lower_bound():
        return "Ω(n²) - must read input"
```

### Lower Bounds in Algebraic Problems

#### 1. Polynomial Evaluation
```python
def polynomial_evaluation_bounds():
    """
    Problem: Evaluate polynomial p(x) = a₀ + a₁x + ... + aₙxⁿ
    
    Horner's method: n multiplications, n additions
    Lower bound: n multiplications (proven optimal)
    
    Proof: Each coefficient aᵢ (i > 0) must multiply some power of x
    """
    
    def horner_method(coefficients, x):
        """Optimal polynomial evaluation"""
        result = coefficients[-1]
        for i in range(len(coefficients) - 2, -1, -1):
            result = result * x + coefficients[i]
        return result
    
    return "Lower bound: n multiplications"
```

#### 2. Fast Fourier Transform (FFT)
```python
def fft_lower_bounds():
    """
    Problem: Compute DFT of n points
    
    FFT algorithm: O(n log n)
    Lower bound: Ω(n log n) for general case
    
    Special cases:
    - Real-valued input: can do better
    - Sparse input: can do better
    """
    
    def fft_complexity():
        return "O(n log n)"
    
    def lower_bound_proof():
        """
        Based on counting argument:
        - n complex outputs from n complex inputs
        - Each output depends on all inputs
        - Information-theoretic argument gives Ω(n log n)
        """
        return "Ω(n log n)"
```

### Applications of Lower Bound Theory

#### 1. Algorithm Design
- **Optimality**: Prove when algorithm is optimal
- **Impossibility**: Show certain performance is impossible
- **Trade-offs**: Understand time vs space trade-offs

#### 2. Complexity Theory
- **P vs NP**: Lower bounds for NP-complete problems
- **Circuit Complexity**: Lower bounds for Boolean circuits
- **Communication Complexity**: Distributed computing limits

#### 3. Practical Applications
- **Database Query Optimization**: Fundamental limits
- **Cryptography**: Security based on computational hardness
- **Machine Learning**: Sample complexity lower bounds

---

## 8. Introduction to Parallel Algorithms - Comprehensive Analysis

### What are Parallel Algorithms?
Parallel algorithms are designed to solve problems using multiple processors simultaneously, dividing the work among processors to achieve faster execution.

### Parallel Computing Models

#### 1. PRAM (Parallel Random Access Machine)
```python
class PRAM:
    """
    Theoretical model for parallel computation
    - Multiple processors with shared memory
    - Synchronous operation
    - Different memory access models
    """
    
    def __init__(self, num_processors, memory_model):
        self.processors = num_processors
        self.model = memory_model  # EREW, CREW, CRCW
    
    def memory_models(self):
        return {
            'EREW': 'Exclusive Read, Exclusive Write',
            'CREW': 'Concurrent Read, Exclusive Write', 
            'CRCW': 'Concurrent Read, Concurrent Write'
        }
```

#### 2. Distributed Memory Model
```python
class DistributedMemory:
    """
    Each processor has private memory
    Communication via message passing
    """
    
    def __init__(self, num_processors):
        self.processors = num_processors
        self.local_memory = [{}] * num_processors
    
    def send_message(self, from_proc, to_proc, data):
        """Message passing between processors"""
        pass
    
    def broadcast(self, source_proc, data):
        """Send data from one processor to all others"""
        pass
```

### Parallel Algorithm Design Techniques

#### 1. Divide and Conquer
```python
def parallel_merge_sort(arr, processors):
    """
    Parallel merge sort using divide and conquer
    
    Time: O(log²n) with O(n) processors
    Work: O(n log n) - same as sequential
    """
    
    if len(arr) <= 1:
        return arr
    
    if processors == 1:
        return sequential_merge_sort(arr)
    
    mid = len(arr) // 2
    left_processors = processors // 2
    right_processors = processors - left_processors
    
    # Parallel recursive calls
    left_sorted = parallel_merge_sort(arr[:mid], left_processors)
    right_sorted = parallel_merge_sort(arr[mid:], right_processors)
    
    # Parallel merge
    return parallel_merge(left_sorted, right_sorted, processors)

def parallel_merge(left, right, processors):
    """Parallel merge of two sorted arrays"""
    if processors == 1:
        return sequential_merge(left, right)
    
    # Divide merge work among processors
    # Each processor handles a portion of the merge
    # Implementation details depend on specific parallel model
    pass
```

#### 2. Parallel Prefix (Scan) Operations
```python
def parallel_prefix_sum(arr, processors):
    """
    Compute prefix sums in parallel
    
    Sequential: O(n)
    Parallel: O(log n) time with O(n) processors
    """
    
    n = len(arr)
    result = arr[:]
    
    # Up-sweep phase
    step = 1
    while step < n:
        # Parallel for loop
        for i in range(step, n, 2 * step):
            if i + step < n:
                result[i + step] += result[i]
        step *= 2
    
    # Down-sweep phase
    result[-1] = 0  # Identity for prefix sum
    step = n // 2
    while step > 0:
        # Parallel for loop
        for i in range(step, n, 2 * step):
            if i + step < n:
                temp = result[i]
                result[i] = result[i + step]
                result[i + step] += temp
        step //= 2
    
    return result
```

#### 3. Parallel Matrix Operations
```python
def parallel_matrix_multiply(A, B, processors):
    """
    Parallel matrix multiplication
    
    Block-based approach:
    - Divide matrices into blocks
    - Assign blocks to processors
    - Compute block products in parallel
    """
    
    n = len(A)
    block_size = n // int(processors ** 0.5)
    
    # Create result matrix
    C = [[0] * n for _ in range(n)]
    
    # Parallel computation of blocks
    for block_i in range(0, n, block_size):
        for block_j in range(0, n, block_size):
            for block_k in range(0, n, block_size):
                # Assign this block computation to a processor
                multiply_block(A, B, C, block_i, block_j, block_k, block_size)
    
    return C

def multiply_block(A, B, C, start_i, start_j, start_k, size):
    """Multiply a block of matrices"""
    for i in range(start_i, min(start_i + size, len(A))):
        for j in range(start_j, min(start_j + size, len(B[0]))):
            for k in range(start_k, min(start_k + size, len(B))):
                C[i][j] += A[i][k] * B[k][j]
```

### Parallel Complexity Analysis

#### 1. Time Complexity
- **T_p(n)**: Time with p processors
- **T_1(n)**: Sequential time
- **Speedup**: S_p = T_1(n) / T_p(n)
- **Efficiency**: E_p = S_p / p

#### 2. Work and Span
```python
def work_span_analysis():
    """
    Work-Span Model:
    - Work (W): Total operations performed
    - Span (S): Length of critical path
    - Parallelism: P = W/S (maximum useful processors)
    
    Brent's Theorem: T_p ≤ W/p + S
    """
    
    examples = {
        'parallel_sum': {
            'work': 'O(n)',
            'span': 'O(log n)',
            'parallelism': 'O(n/log n)'
        },
        'parallel_merge_sort': {
            'work': 'O(n log n)',
            'span': 'O(log² n)',
            'parallelism': 'O(n/log n)'
        }
    }
    
    return examples
```

### Specific Parallel Algorithms

#### 1. Parallel Sorting
```python
def parallel_quicksort(arr, processors):
    """
    Parallel quicksort
    
    Average case: O(log n) time with O(n) processors
    Worst case: O(n) time (unbalanced partitions)
    """
    
    if len(arr) <= 1 or processors == 1:
        return sequential_quicksort(arr)
    
    # Choose pivot (can be done in parallel)
    pivot = choose_pivot(arr)
    
    # Parallel partition
    left, right = parallel_partition(arr, pivot, processors)
    
    # Recursive parallel calls
    left_processors = processors // 2
    right_processors = processors - left_processors
    
    left_sorted = parallel_quicksort(left, left_processors)
    right_sorted = parallel_quicksort(right, right_processors)
    
    return left_sorted + [pivot] + right_sorted

def parallel_partition(arr, pivot, processors):
    """Partition array in parallel around pivot"""
    # Each processor handles a portion of array
    # Use parallel prefix to determine final positions
    pass
```

#### 2. Parallel Graph Algorithms
```python
def parallel_bfs(graph, start, processors):
    """
    Parallel Breadth-First Search
    
    Time: O(diameter × log n) with O(n + m) processors
    where diameter is the longest shortest path
    """
    
    n = len(graph)
    visited = [False] * n
    distance = [-1] * n
    current_level = [start]
    
    visited[start] = True
    distance[start] = 0
    level = 0
    
    while current_level:
        next_level = []
        
        # Parallel processing of current level
        for vertex in current_level:
            # Process neighbors in parallel
            neighbors = parallel_get_neighbors(graph, vertex, processors)
            
            for neighbor in neighbors:
                if not visited[neighbor]:
                    visited[neighbor] = True
                    distance[neighbor] = level + 1
                    next_level.append(neighbor)
        
        current_level = next_level
        level += 1
    
    return distance

def parallel_connected_components(graph, processors):
    """
    Find connected components in parallel
    
    Using pointer jumping technique:
    Time: O(log n) with O(n + m) processors
    """
    
    n = len(graph)
    parent = list(range(n))  # Initially each vertex is its own parent
    
    # Parallel pointer jumping
    while True:
        changed = False
        
        # Parallel for each vertex
        for v in range(n):
            if parent[parent[v]] != parent[v]:
                parent[v] = parent[parent[v]]
                changed = True
        
        if not changed:
            break
    
    return parent
```

#### 3. Parallel Numerical Algorithms
```python
def parallel_matrix_vector_multiply(matrix, vector, processors):
    """
    Parallel matrix-vector multiplication
    
    Time: O(n²/p + log p) with p processors
    Communication: O(n) per processor
    """
    
    n = len(matrix)
    result = [0] * n
    rows_per_processor = n // processors
    
    # Each processor computes a portion of result
    for proc in range(processors):
        start_row = proc * rows_per_processor
        end_row = min((proc + 1) * rows_per_processor, n)
        
        # Processor proc computes result[start_row:end_row]
        for i in range(start_row, end_row):
            result[i] = sum(matrix[i][j] * vector[j] for j in range(n))
    
    return result

def parallel_gaussian_elimination(matrix, processors):
    """
    Parallel Gaussian elimination
    
    Time: O(n³/p + n² log p) with p processors
    """
    
    n = len(matrix)
    
    for k in range(n):
        # Find pivot in parallel
        pivot_row = parallel_find_pivot(matrix, k, processors)
        
        # Swap rows if necessary
        if pivot_row != k:
            matrix[k], matrix[pivot_row] = matrix[pivot_row], matrix[k]
        
        # Parallel elimination
        for i in range(k + 1, n):
            factor = matrix[i][k] / matrix[k][k]
            
            # Parallel row operations
            for j in range(k, n):
                matrix[i][j] -= factor * matrix[k][j]
    
    return matrix
```

### Parallel Algorithm Design Patterns

#### 1. Map-Reduce Pattern
```python
def map_reduce_pattern(data, map_func, reduce_func, processors):
    """
    Generic map-reduce pattern
    
    1. Map: Apply function to each data element in parallel
    2. Reduce: Combine results using associative operation
    """
    
    # Map phase - parallel
    mapped_data = []
    chunk_size = len(data) // processors
    
    for proc in range(processors):
        start = proc * chunk_size
        end = min((proc + 1) * chunk_size, len(data))
        chunk_result = [map_func(item) for item in data[start:end]]
        mapped_data.extend(chunk_result)
    
    # Reduce phase - parallel tree reduction
    return parallel_reduce(mapped_data, reduce_func, processors)

def parallel_reduce(data, reduce_func, processors):
    """Parallel reduction using tree structure"""
    if len(data) == 1:
        return data[0]
    
    # Pair up elements and reduce in parallel
    next_level = []
    for i in range(0, len(data), 2):
        if i + 1 < len(data):
            next_level.append(reduce_func(data[i], data[i + 1]))
        else:
            next_level.append(data[i])
    
    return parallel_reduce(next_level, reduce_func, processors)
```

#### 2. Pipeline Pattern
```python
def pipeline_pattern(data, stages, processors):
    """
    Pipeline parallel processing
    
    Different stages of computation overlap
    Useful for streaming data processing
    """
    
    stage_processors = processors // len(stages)
    pipeline_buffer = [[] for _ in stages]
    
    for item in data:
        current_item = item
        
        # Pass through pipeline stages
        for stage_idx, stage_func in enumerate(stages):
            # Process in parallel within each stage
            current_item = stage_func(current_item)
            pipeline_buffer[stage_idx].append(current_item)
    
    return pipeline_buffer[-1]  # Final stage output
```

### Performance Analysis and Optimization

#### 1. Amdahl's Law
```python
def amdahls_law(sequential_fraction, processors):
    """
    Amdahl's Law: Maximum speedup with parallel processing
    
    Speedup = 1 / (sequential_fraction + (1 - sequential_fraction) / processors)
    
    Shows that sequential portions limit parallel speedup
    """
    
    speedup = 1 / (sequential_fraction + (1 - sequential_fraction) / processors)
    return speedup

def demonstrate_amdahls_law():
    """Demonstrate impact of sequential fraction"""
    processors = [1, 2, 4, 8, 16, 32, 64]
    sequential_fractions = [0.1, 0.2, 0.5, 0.9]
    
    for seq_frac in sequential_fractions:
        print(f"Sequential fraction: {seq_frac}")
        for p in processors:
            speedup = amdahls_law(seq_frac, p)
            print(f"  {p} processors: {speedup:.2f}x speedup")
```

#### 2. Load Balancing
```python
def dynamic_load_balancing(tasks, processors):
    """
    Dynamic load balancing for irregular workloads
    
    Work-stealing approach:
    - Each processor maintains local task queue
    - Idle processors steal work from busy ones
    """
    
    task_queues = [[] for _ in range(processors)]
    
    # Initial distribution
    for i, task in enumerate(tasks):
        task_queues[i % processors].append(task)
    
    # Simulate work-stealing
    while any(queue for queue in task_queues):
        for proc in range(processors):
            if not task_queues[proc]:
                # Steal work from another processor
                for other_proc in range(processors):
                    if len(task_queues[other_proc]) > 1:
                        stolen_task = task_queues[other_proc].pop()
                        task_queues[proc].append(stolen_task)
                        break
```

### Applications of Parallel Algorithms

#### 1. Scientific Computing
- **Numerical Simulations**: Weather prediction, fluid dynamics
- **Linear Algebra**: Large matrix operations
- **Monte Carlo Methods**: Statistical simulations

#### 2. Data Processing
- **Big Data Analytics**: MapReduce, Spark
- **Database Operations**: Parallel query processing
- **Machine Learning**: Parallel training algorithms

#### 3. Graphics and Multimedia
- **Image Processing**: Parallel filters, transformations
- **Computer Graphics**: Ray tracing, rendering
- **Video Processing**: Parallel encoding/decoding

---

## 9. Comparison of Techniques - Comprehensive Analysis

### Backtracking vs Branch & Bound vs Dynamic Programming

| Aspect | Backtracking | Branch & Bound | Dynamic Programming |
|--------|--------------|----------------|-------------------|
| **Search Strategy** | Depth-first | Best-first | Bottom-up/Top-down |
| **Pruning Method** | Constraint violation | Bound comparison | None (avoids recomputation) |
| **Problem Type** | Feasibility/Enumeration | Optimization | Optimization |
| **Memory Usage** | O(depth) | O(queue size) | O(state space) |
| **Optimality** | Finds any solution | Finds optimal solution | Finds optimal solution |
| **When to Use** | Constraint satisfaction | NP-hard optimization | Overlapping subproblems |

### Algorithm Selection Guide

#### Choose Backtracking When:
1. **Constraint Satisfaction**: N-Queens, Sudoku, Graph Coloring
2. **Feasibility Questions**: "Does a solution exist?"
3. **Enumeration**: Find all valid solutions
4. **Strong Pruning**: Constraints eliminate many branches early

#### Choose Branch & Bound When:
1. **Optimization Problems**: Need optimal solution
2. **Good Bounds Available**: Can compute tight bounds efficiently
3. **NP-Hard Problems**: Exact solution needed despite complexity
4. **Moderate Problem Size**: Practical for instances that fit in memory

#### Choose Dynamic Programming When:
1. **Optimal Substructure**: Problem breaks into optimal subproblems
2. **Overlapping Subproblems**: Same subproblems solved repeatedly
3. **Polynomial Solutions**: Can solve in polynomial time
4. **Clear Recurrence**: Can express solution recursively

### Performance Comparison

#### Time Complexity Comparison
```python
def complexity_comparison():
    """
    Problem: 0/1 Knapsack with n items, capacity W
    
    Backtracking: O(2^n) - try all subsets
    Branch & Bound: O(2^n) worst case, much better average
    Dynamic Programming: O(nW) - polynomial
    
    For large W, DP may not be practical (pseudo-polynomial)
    For small W, DP is clearly best
    For optimization with good bounds, B&B often practical
    """
    
    return {
        'backtracking': 'O(2^n)',
        'branch_bound': 'O(2^n) worst, better average',
        'dynamic_programming': 'O(nW)'
    }
```

#### Space Complexity Comparison
```python
def space_comparison():
    """
    Backtracking: O(n) - recursion stack
    Branch & Bound: O(2^n) worst case - priority queue
    Dynamic Programming: O(nW) - DP table
    
    Backtracking uses least space
    DP space can be optimized to O(W) for knapsack
    B&B space depends on branching factor and pruning effectiveness
    """
    
    return {
        'backtracking': 'O(depth)',
        'branch_bound': 'O(queue_size)',
        'dynamic_programming': 'O(state_space)'
    }
```

---

## 10. Practice Problems and Detailed Solutions

### Problem 1: 8-Queens Backtracking (Exam Style)

**Problem**: Solve the 8-Queens problem and show the first solution found.

**Solution**:
```python
def solve_8_queens():
    board = [-1] * 8
    
    def is_safe(row, col):
        for i in range(row):
            if (board[i] == col or 
                board[i] - i == col - row or 
                board[i] + i == col + row):
                return False
        return True
    
    def backtrack(row):
        if row == 8:
            return True
        
        for col in range(8):
            if is_safe(row, col):
                board[row] = col
                if backtrack(row + 1):
                    return True
        return False
    
    if backtrack(0):
        return board
    return None

# First solution: [0, 4, 7, 5, 2, 6, 1, 3]
```

### Problem 2: Graph Coloring (June 2024 Exam)

**Problem**: Color the given 6-vertex graph with minimum colors.

**Solution**: (Already solved in detail in Section 4)
- **Answer**: 3 colors needed
- **Coloring**: a=1, b=2, c=3, d=1, e=2, f=3

### Problem 3: TSP Branch & Bound

**Problem**: Solve TSP for 4 cities using Branch & Bound.

**Solution**: (Already solved in detail in Section 6)
- **Optimal Tour**: 0→1→3→2→0 or 0→2→3→1→0
- **Minimum Cost**: 80

### Problem 4: Hamiltonian Cycle Detection

**Problem**: Determine if given graph has Hamiltonian cycle.

**Solution**: Use backtracking algorithm from Section 3.

### Problem 5: Parallel Algorithm Design

**Problem**: Design parallel algorithm for finding maximum element.

**Solution**:
```python
def parallel_max(arr, processors):
    """
    Parallel maximum finding
    Time: O(log n) with O(n) processors
    """
    
    n = len(arr)
    if n == 1:
        return arr[0]
    
    # Divide array among processors
    chunk_size = n // processors
    local_maxes = []
    
    # Each processor finds local maximum
    for p in range(processors):
        start = p * chunk_size
        end = min((p + 1) * chunk_size, n)
        local_max = max(arr[start:end])
        local_maxes.append(local_max)
    
    # Parallel reduction to find global maximum
    while len(local_maxes) > 1:
        next_level = []
        for i in range(0, len(local_maxes), 2):
            if i + 1 < len(local_maxes):
                next_level.append(max(local_maxes[i], local_maxes[i + 1]))
            else:
                next_level.append(local_maxes[i])
        local_maxes = next_level
    
    return local_maxes[0]
```

---

## Summary and Exam Preparation

### Key Concepts to Master

#### 1. Backtracking
- **Template**: Understand the general backtracking structure
- **Constraint Checking**: Efficient pruning conditions
- **State Representation**: How to represent partial solutions
- **Examples**: 8-Queens, Graph Coloring, Hamiltonian Cycle

#### 2. Branch & Bound
- **Bounding Functions**: How to compute tight bounds
- **Search Strategy**: Best-first vs depth-first
- **Pruning**: When to eliminate branches
- **Examples**: TSP, 0/1 Knapsack

#### 3. Lower Bounds
- **Proof Techniques**: Counting, adversary, reduction arguments
- **Information Theory**: log₂(n!) bounds for sorting
- **Practical Impact**: When algorithms are optimal

#### 4. Parallel Algorithms
- **Models**: PRAM, distributed memory
- **Complexity**: Work, span, speedup, efficiency
- **Patterns**: Divide-conquer, map-reduce, pipeline
- **Limitations**: Amdahl's law, communication overhead

### Problem-Solving Strategy

#### 1. Problem Recognition
- **Backtracking**: Constraint satisfaction, enumeration
- **Branch & Bound**: Optimization with good bounds
- **Parallel**: Independent subproblems, regular structure

#### 2. Algorithm Design
- **State Space**: How to represent solutions
- **Constraints**: What makes solutions valid
- **Optimization**: What to minimize/maximize
- **Parallelization**: How to divide work

#### 3. Analysis
- **Time Complexity**: Worst, average, best case
- **Space Complexity**: Memory requirements
- **Optimality**: Is solution guaranteed optimal?
- **Scalability**: How does performance change with input size?

### Exam Tips

#### 1. Practice Problems
- Work through examples step-by-step
- Trace algorithm execution manually
- Understand why pruning works
- Calculate complexity bounds

#### 2. Implementation
- Know the basic templates
- Understand key optimizations
- Be able to modify for variants
- Debug common mistakes

#### 3. Theory
- Prove lower bounds using standard techniques
- Understand parallel complexity measures
- Compare different approaches
- Know when each technique applies

---

*This comprehensive unit covers all backtracking, branch & bound, lower bound theory, and parallel algorithm concepts tested in CS/SD-402 examinations, with detailed examples, complete implementations, and thorough analysis of each technique.*