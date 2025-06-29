# Unit II: Greedy Strategy and Algorithms

## 0. Syllabus
Study of Greedy strategy, examples of greedy method like optimal merge patterns, Huffman coding, minimum spanning trees, knapsack problem, job sequencing with deadlines, single source shortest path algorithm.

## 1. Introduction to Greedy Strategy

### What is Greedy Strategy?
```
┌─────────────────────────────────────────────────────────────┐
│                    GREEDY STRATEGY                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  A problem-solving approach that makes the locally optimal │
│  choice at each step, hoping to find a global optimum      │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 KEY PRINCIPLE                           │ │
│  │                                                         │ │
│  │  "Make the best choice available at the moment"        │ │
│  │                                                         │ │
│  │  • Choose locally optimal solution                     │ │
│  │  • Never reconsider previous choices                   │ │
│  │  • Hope local optimum leads to global optimum          │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  DECISION TREE                          │ │
│  │                                                         │ │
│  │                    Start                                │ │
│  │                   /  |  \                              │ │
│  │               Choice1 Choice2 Choice3                   │ │
│  │                 ✓                                       │ │
│  │               (Best)                                    │ │
│  │                 |                                       │ │
│  │            Next Choices                                 │ │
│  │              /    \                                     │ │
│  │          ChoiceA  ChoiceB                               │ │
│  │             ✓                                           │ │
│  │           (Best)                                        │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Characteristics of Greedy Algorithms
```
┌─────────────────────────────────────────────────────────────┐
│               GREEDY CHARACTERISTICS                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Greedy    │  │   Local     │  │ Irrevocable │         │
│  │   Choice    │  │  Optimum    │  │   Choices   │         │
│  │             │  │             │  │             │         │
│  │ • Best      │  │ • Choose    │  │ • Cannot    │         │
│  │   available │  │   best at   │  │   undo      │         │
│  │   option    │  │   current   │  │   decision  │         │
│  │ • No future │  │   step      │  │ • Commit to │         │
│  │   lookahead │  │ • Immediate │  │   decision  │         │
│  │             │  │   benefit   │  │   forward   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Simple    │  │  Efficient  │  │   Fast      │         │
│  │             │  │             │  │             │         │
│  │ • Easy to   │  │ • Usually   │  │ • Quick     │         │
│  │   implement │  │   O(n log n)│  │   decisions │         │
│  │ • Clear     │  │   or better │  │ • No        │         │
│  │   logic     │  │ • Low space │  │   backtrack │         │
│  │ • Intuitive │  │   usage     │  │ • Linear    │         │
│  │             │  │             │  │   progress  │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

### Greedy vs Other Approaches
```
┌─────────────────────────────────────────────────────────────┐
│                APPROACH COMPARISON                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 GREEDY METHOD                           │ │
│  │                                                         │ │
│  │  Pros:                                                  │ │
│  │  • Simple and fast                                     │ │
│  │  • Easy to implement                                   │ │
│  │  • Good for many optimization problems                 │ │
│  │                                                         │ │
│  │  Cons:                                                  │ │
│  │  • May not always give optimal solution                │ │
│  │  • Hard to prove correctness                           │ │
│  │  • Cannot undo decisions                               │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              DYNAMIC PROGRAMMING                        │ │
│  │                                                         │ │
│  │  • Considers all possible solutions                     │ │
│  │  • Guarantees optimal solution                          │ │
│  │  • Higher time complexity                               │ │
│  │  • Uses memoization/tabulation                          │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 DIVIDE & CONQUER                        │ │
│  │                                                         │ │
│  │  • Breaks problem into subproblems                      │ │
│  │  • Combines solutions                                   │ │
│  │  • Recursive approach                                   │ │
│  │  • Good for certain problem types                       │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### General Greedy Algorithm Template
```
┌─────────────────────────────────────────────────────────────┐
│                GREEDY ALGORITHM TEMPLATE                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Algorithm: GreedyAlgorithm(input)                          │
│  {                                                          │
│      solution = empty                                       │
│      while (not all elements processed) {                   │
│          candidate = selectBestCandidate(remaining)         │
│          if (isFeasible(candidate, solution)) {             │
│              solution = solution ∪ candidate                │
│          }                                                  │
│          remove candidate from remaining                    │
│      }                                                      │
│      return solution                                        │
│  }                                                          │
│                                                             │
│  Key Functions:                                            │
│  • selectBestCandidate(): Choose locally best option       │
│  • isFeasible(): Check if choice is valid                  │
│  • solution construction: Build final answer               │
│                                                             │
│  Steps:                                                    │
│  1. Define greedy choice criterion                         │
│  2. Prove greedy choice property                           │
│  3. Prove optimal substructure                             │
│  4. Implement algorithm                                     │
└─────────────────────────────────────────────────────────────┘
```

### When Does Greedy Work?
```
┌─────────────────────────────────────────────────────────────┐
│               GREEDY ALGORITHM CONDITIONS                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              GREEDY CHOICE PROPERTY                     │ │
│  │                                                         │ │
│  │  A global optimum can be arrived at by making a        │ │
│  │  locally optimal (greedy) choice                       │ │
│  │                                                         │ │
│  │  • Local best choice leads to global best              │ │
│  │  • No need to consider consequences of choice          │ │
│  │  • Current choice doesn't affect future choices        │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │             OPTIMAL SUBSTRUCTURE                        │ │
│  │                                                         │ │
│  │  An optimal solution to the problem contains            │ │
│  │  optimal solutions to subproblems                       │ │
│  │                                                         │ │
│  │  • Problem can be broken into subproblems              │ │
│  │  • Optimal solution uses optimal solutions of parts    │ │
│  │  • Subproblems are independent                          │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Examples where Greedy works:                              │
│  • Fractional Knapsack                                     │
│  • Activity Selection                                       │
│  • Huffman Coding                                          │
│  • Minimum Spanning Tree (MST)                             │
│  • Single Source Shortest Path (Dijkstra)                  │
└─────────────────────────────────────────────────────────────┘
```

## 2. Optimal Merge Patterns

### Problem Statement
```
┌─────────────────────────────────────────────────────────────┐
│                 OPTIMAL MERGE PATTERNS                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Problem: Given n sorted files, merge them into a single   │
│  sorted file with minimum number of comparisons            │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   SCENARIO                              │ │
│  │                                                         │ │
│  │  Files: F1(size=20), F2(size=30), F3(size=10), F4(size=5)│ │
│  │                                                         │ │
│  │  Goal: Merge all files into one sorted file             │
│  │  Constraint: Can only merge 2 files at a time          │
│  │  Objective: Minimize total merge cost                   │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Key Insight: Cost of merging two files = sum of their     │
│  sizes (need to examine all elements)                      │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                MERGE COST EXAMPLE                       │ │
│  │                                                         │ │
│  │  Merge F1(20) + F2(30) = Cost: 20 + 30 = 50           │ │
│  │  Result: F12(50)                                        │ │
│  │                                                         │ │
│  │  Merge F12(50) + F3(10) = Cost: 50 + 10 = 60          │ │
│  │  Result: F123(60)                                       │ │
│  │                                                         │ │
│  │  Merge F123(60) + F4(5) = Cost: 60 + 5 = 65           │ │
│    │  Total Cost: 50 + 60 + 65 = 175                        │ │
│  │  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Greedy Strategy for Optimal Merge
```
┌─────────────────────────────────────────────────────────────┐
│                    GREEDY APPROACH                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Strategy: Always merge the two smallest files first       │
│                                                             │
│  Algorithm: OptimalMerge(sizes[1..n])                      │
│  {                                                          │
│      create min-heap with all file sizes                   │
│      totalCost = 0                                         │
│                                                             │
│      while (heap has more than 1 element) {                │
│          size1 = extractMin(heap)                          │
│          size2 = extractMin(heap)                          │
│          mergeCost = size1 + size2                         │
│          totalCost += mergeCost                            │
│          insert(heap, mergeCost)                           │
│      }                                                      │
│                                                             │
│      return totalCost                                      │
│  }                                                          │
│                                                             │
│  Time Complexity: O(n log n)                              │
│  Space Complexity: O(n)                                   │
└─────────────────────────────────────────────────────────────┘
```

### Example: Step-by-Step Execution
```
┌─────────────────────────────────────────────────────────────┐
│                 OPTIMAL MERGE EXAMPLE                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Input Files: F1(20), F2(30), F3(10), F4(5)              │
│                                                             │
│  Step 1: Create min-heap [5, 10, 20, 30]                  │
│                                                             │
│  Step 2: Extract two smallest (5, 10)                     │
│  Merge cost: 5 + 10 = 15                                  │
│  Total cost: 15                                           │
│  Heap: [15, 20, 30]                                       │
│                                                             │
│  Step 3: Extract two smallest (15, 20)                    │
│  Merge cost: 15 + 20 = 35                                 │
│  Total cost: 15 + 35 = 50                                 │
│  Heap: [30, 35]                                           │
│                                                             │
│  Step 4: Extract remaining two (30, 35)                   │
│  Merge cost: 30 + 35 = 65                                 │
│  Total cost: 15 + 35 + 65 = 115                          │
│                                                             │
│  Final Answer: Minimum merge cost = 115                    │
│                                                             │
│  Merge Tree:                                               │
│                     (65)                                   │
│                   /      \                                 │
│                F2(30)    (35)                              │
│                         /    \                             │
│                       (15)   F1(20)                        │
│                      /    \                                │
│                    F4(5)  F3(10)                           │
└─────────────────────────────────────────────────────────────┘
```

## 3. Huffman Coding

### Problem Statement
```
┌─────────────────────────────────────────────────────────────┐
│                    HUFFMAN CODING                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Problem: Given characters and their frequencies, design   │
│  an optimal prefix-free binary code to minimize total      │
│  encoding length                                            │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 PREFIX-FREE CODE                        │ │
│  │                                                         │ │
│  │  No codeword is a prefix of another codeword            │ │
│  │                                                         │ │
│  │  Example:                                               │ │
│  │  A: 00    ✓ (Valid - no conflicts)                     │ │
│  │  B: 01                                                  │ │
│  │  C: 10                                                  │ │
│  │  D: 11                                                  │ │
│  │                                                         │ │
│  │  A: 0     ✗ (Invalid - A is prefix of others)          │ │
│  │  B: 01                                                  │ │
│  │  C: 10                                                  │ │
│  │ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Goal: Minimize Σ(frequency[i] × codeLength[i])            │
└─────────────────────────────────────────────────────────────┘
```

### Huffman Algorithm
```
┌─────────────────────────────────────────────────────────────┐
│                 HUFFMAN ALGORITHM                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Algorithm: HuffmanCode(characters, frequencies)           │
│  {                                                          │
│      // Create leaf nodes for each character               │
│      create min-heap of nodes                              │
│      for each character c with frequency f {               │
│          create node(c, f)                                 │
│          insert node into heap                             │
│      }                                                      │
│                                                             │
│      // Build Huffman tree                                 │
│      while (heap has more than 1 node) {                   │
│          left = extractMin(heap)                           │
│          right = extractMin(heap)                          │
│          merged = createNode(null, left.freq + right.freq) │
│          merged.left = left                                │
│          merged.right = right                              │
│          insert(heap, merged)                              │
│      }                                                      │
│                                                             │
│      root = extractMin(heap)                               │
│      generateCodes(root, "")                               │
│  }                                                          │
│                                                             │
│  generateCodes(node, code) {                               │
│      if (node is leaf) {                                   │
│          node.code = code                                  │
│      } else {                                               │
│          generateCodes(node.left, code + "0")              │
│          generateCodes(node.right, code + "1")             │
│      }                                                      │
│  }                                                          │
└─────────────────────────────────────────────────────────────┘
```

### Huffman Coding Example
```
┌─────────────────────────────────────────────────────────────┐
│                HUFFMAN CODING EXAMPLE                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Characters and Frequencies:                               │
│  A: 45, B: 13, C: 12, D: 16, E: 9, F: 5                  │
│                                                             │
│  Step 1: Create initial min-heap                           │
│  [F:5, E:9, C:12, B:13, D:16, A:45]                       │
│                                                             │
│  Step 2: Merge F(5) and E(9)                              │
│  Cost: 5 + 9 = 14                                         │
│  Heap: [C:12, B:13, FE:14, D:16, A:45]                    │
│                                                             │
│       (14)                                                 │
│      /    \                                                │
│    F(5)  E(9)                                              │
│                                                             │
│  Step 3: Merge C(12) and B(13)                            │
│  Cost: 12 + 13 = 25                                       │
│  Heap: [FE:14, D:16, CB:25, A:45]                         │
│                                                             │
│       (25)                                                 │
│      /    \                                                │
│    C(12) B(13)                                             │
│                                                             │
│  Step 4: Merge FE(14) and D(16)                           │
│  Cost: 14 + 16 = 30                                       │
│  Heap: [CB:25, FED:30, A:45]                              │
│                                                             │
│         (30)                                               │
│        /    \                                              │
│      (14)   D(16)                                          │
│     /    \                                                 │
│   F(5)  E(9)                                               │
│                                                             │
│  Step 5: Merge CB(25) and FED(30)                         │
│  Cost: 25 + 30 = 55                                       │
│  Heap: [A:45, CBFED:55]                                    │
│                                                             │
│  Step 6: Final merge A(45) and CBFED(55)                  │
│  Final tree:                                               │
│                                                             │
│                     (100)                                  │
│                    /     \                                 │
│                  A(45)   (55)                              │
│                         /    \                             │
│                      (25)    (30)                          │
│                     /   \   /    \                         │
│                  C(12) B(13) (14) D(16)                    │
│                              /  \                          │
│                            F(5) E(9)                       │
│                                                             │
│  Generated Codes:                                          │
│  A: 0, C: 100, B: 101, F: 1100, E: 1101, D: 111          │
└─────────────────────────────────────────────────────────────┘
```

### Cost Calculation
```
┌─────────────────────────────────────────────────────────────┐
│                   COST CALCULATION                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Huffman Code Costs:                                       │
│  A: freq=45, code=0 (length=1)      → 45 × 1 = 45         │
│  C: freq=12, code=100 (length=3)    → 12 × 3 = 36         │
│  B: freq=13, code=101 (length=3)    → 13 × 3 = 39         │
│  F: freq=5, code=1100 (length=4)    → 5 × 4 = 20          │
│  E: freq=9, code=1101 (length=4)    → 9 × 4 = 36          │
│  D: freq=16, code=111 (length=3)    → 16 × 3 = 48         │
│                                                             │
│  Total Huffman Cost: 45+36+39+20+36+48 = 224              │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │            COMPARISON WITH FIXED-LENGTH                 │ │
│  │                                                         │ │
│  │  Fixed-length code (3 bits per character):             │ │
│  │  A: 000, B: 001, C: 010, D: 011, E: 100, F: 101       │ │
│  │                                                         │ │
│  │  Fixed-length cost:                                    │ │
│  │  (45+13+12+16+9+5) × 3 = 100 × 3 = 300                │ │
│  │                                                         │ │
│    │  Savings: 300 - 224 = 76 (25.3% reduction)            │ │
│  │  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 4. Minimum Spanning Trees (MST)

### Problem Statement
```
┌─────────────────────────────────────────────────────────────┐
│                MINIMUM SPANNING TREE                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Problem: Given a connected, undirected graph with         │
│  weighted edges, find a spanning tree with minimum         │
│  total edge weight                                          │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 DEFINITIONS                             │ │
│  │                                                         │ │
│  │  Spanning Tree: Tree that includes ALL vertices        │ │
│  │  • Connected subgraph                                  │ │
│  │  • No cycles                                           │ │
│  │  • (V-1) edges for V vertices                          │ │
│  │                                                         │ │
│  │  Minimum Spanning Tree: Spanning tree with minimum     │ │
│  │  sum of edge weights                                   │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Applications:                                             │
│  • Network design (cable laying, pipeline)                │
│  • Clustering algorithms                                   │
│  • Approximation algorithms                               │
│  • Circuit design                                         │
└─────────────────────────────────────────────────────────────┘
```

### Kruskal's Algorithm
```
┌─────────────────────────────────────────────────────────────┐
│                   KRUSKAL'S ALGORITHM                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Strategy: Select edges in order of increasing weight,     │
│  add edge if it doesn't create a cycle                     │
│                                                             │
│  Algorithm: Kruskal(Graph G)                              │
│  {                                                          │
│      MST = ∅                                               │
│      sort all edges by weight (ascending)                  │
│      initialize Union-Find structure                       │
│                                                             │
│      for each edge (u,v) in sorted order {                 │
│          if (find(u) ≠ find(v)) {                          │
│              MST = MST ∪ {(u,v)}                           │
│              union(u, v)                                   │
│          }                                                  │
│      }                                                      │
│      return MST                                            │
│  }                                                          │
│                                                             │
│  Time Complexity: O(E log E)                              │
│  • Sorting edges: O(E log E)                              │
│  • Union-Find operations: O(α(V)) ≈ O(1)                  │
│                                                             │
│  Space Complexity: O(V) for Union-Find structure          │
└─────────────────────────────────────────────────────────────┘
```

### Prim's Algorithm
```
┌─────────────────────────────────────────────────────────────┐
│                    PRIM'S ALGORITHM                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Strategy: Grow MST one vertex at a time, always adding    │
│  minimum weight edge connecting MST to non-MST vertex      │
│                                                             │
│  Algorithm: Prim(Graph G, start vertex s)                  │
│  {                                                          │
│      MST = ∅                                               │
│      visited = {s}                                         │
│      create priority queue of edges from s                 │
│                                                             │
│      while (|visited| < |V|) {                             │
│          (u,v,weight) = extractMin(priority_queue)         │
│          if (v ∉ visited) {                                │
│              MST = MST ∪ {(u,v)}                           │
│              visited = visited ∪ {v}                       │
│              add all edges from v to priority_queue        │
│          }                                                  │
│      }                                                      │
│      return MST                                            │
│  }                                                          │
│                                                             │
│  Time Complexity:                                          │
│  • Using Binary Heap: O(E log V)                          │
│  • Using Fibonacci Heap: O(E + V log V)                   │
│                                                             │
│  Space Complexity: O(V) for visited set and heap          │
└─────────────────────────────────────────────────────────────┘
```

### MST Example: Kruskal's Algorithm
```
┌─────────────────────────────────────────────────────────────┐
│               KRUSKAL'S ALGORITHM EXAMPLE                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Input Graph:                                              │
│                                                             │
│      A ------4------ B                                     │
│      |\\             |                                     │
│      | \\           |                                      │
│      |  8\\         |1                                     │
│      |    \\        |                                      │
│      |     \\       |                                      │
│      2       11     |                                      │
│      |         \\   |                                      │
│      |          \\  |                                      │
│      |           \\ |                                      │
│      C ------7------ D                                     │
│      |               |                                     │
│      |6             |5                                     │
│      |               |                                     │
│      E ------3------ F                                     │
│                                                             │
│  Edge List (sorted by weight):                             │
│  (B,D): 1, (A,C): 2, (E,F): 3, (A,B): 4, (D,F): 5,       │
│  (C,E): 6, (C,D): 7, (A,C): 8, (C,D): 11                  │
│                                                             │
│  Step-by-step execution:                                   │
│                                                             │
│  1. Add (B,D): 1  [No cycle] - MST = {(B,D)}              │
│     Union-Find: {A}, {B,D}, {C}, {E}, {F}                 │
│                                                             │
│  2. Add (A,C): 2  [No cycle] - MST = {(B,D), (A,C)}       │
│     Union-Find: {A,C}, {B,D}, {E}, {F}                    │
│                                                             │
│  3. Add (E,F): 3  [No cycle] - MST = {(B,D), (A,C), (E,F)}│
│     Union-Find: {A,C}, {B,D}, {E,F}                       │
│                                                             │
│  4. Add (A,B): 4  [No cycle] - MST = {..., (A,B)}         │
│     Union-Find: {A,B,C,D}, {E,F}                          │
│                                                             │
│  5. Add (D,F): 5  [No cycle] - MST = {..., (D,F)}         │
│     Union-Find: {A,B,C,D,E,F} - All connected             │
│                                                             │
│  6. Skip (C,E): 6 [Would create cycle]                    │
│                                                             │
│  Final MST:                                                │
│      A ------4------ B                                     │
│      |               |                                     │
│      |               |                                     │
│      |               |1                                    │
│      |               |                                     │
│      |               |                                     │
│      2               |                                     │
│      |               |                                     │
│      |               |                                     │
│      |               |                                     │
│      C               D                                     │
│                      |                                     │
│                     |5                                     │
│                      |                                     │
│      E ------3------ F                                     │
│                                                             │
│  │  Total weight: 1 + 2 + 3 + 4 + 5 = 15                     │
└─────────────────────────────────────────────────────────────┘
```

## 5. Knapsack Problem (Fractional)

### Problem Statement
```
┌─────────────────────────────────────────────────────────────┐
│               FRACTIONAL KNAPSACK PROBLEM                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Problem: Given n items with weights and values, and a     │
│  knapsack of capacity W, maximize the total value by       │
│  selecting items (fractions allowed)                       │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    INPUT                                │ │
│  │                                                         │ │
│  │  Items: (weight, value)                                 │ │
│  │  Item 1: (w₁, v₁)                                       │ │
│  │  Item 2: (w₂, v₂)                                       │ │
│  │  ...                                                    │ │
│  │  Item n: (wₙ, vₙ)                                       │ │
│  │                                                         │ │
│  │  Knapsack capacity: W                                   │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Key Difference: Unlike 0/1 knapsack, we can take          │
│  fractions of items                                         │
│                                                             │
│  Objective: Maximize Σ(xᵢ × vᵢ) subject to Σ(xᵢ × wᵢ) ≤ W │
│  where 0 ≤ xᵢ ≤ 1 (fraction of item i)                    │
└─────────────────────────────────────────────────────────────┘
```

### Greedy Strategy
```
┌─────────────────────────────────────────────────────────────┐
│                 GREEDY APPROACH                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Strategy: Sort items by value-to-weight ratio in          │
│  descending order, then fill knapsack greedily             │
│                                                             │
│  Algorithm: FractionalKnapsack(items[], W)                 │
│  {                                                          │
│      // Calculate value-to-weight ratio for each item      │
│      for each item i {                                     │
│          ratio[i] = value[i] / weight[i]                   │
│      }                                                      │
│                                                             │
│      // Sort items by ratio in descending order            │
│      sort items by ratio (descending)                      │
│                                                             │
│      totalValue = 0                                        │
│      remainingCapacity = W                                 │
│                                                             │
│      for each item i in sorted order {                     │
│          if (weight[i] <= remainingCapacity) {             │
│              // Take entire item                           │
│              totalValue += value[i]                        │
│              remainingCapacity -= weight[i]                │
│          } else {                                           │
│              // Take fraction of item                      │
│              fraction = remainingCapacity / weight[i]      │
│              totalValue += fraction × value[i]             │
│              break                                          │
│          }                                                  │
│      }                                                      │
│      return totalValue                                     │
│  }                                                          │
│                                                             │
│  Time Complexity: O(n log n) - dominated by sorting        │
│  Space Complexity: O(1) if sorting in-place               │
└─────────────────────────────────────────────────────────────┘
```

### Example: Fractional Knapsack
```
┌─────────────────────────────────────────────────────────────┐
│             FRACTIONAL KNAPSACK EXAMPLE                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Input:                                                     │
│  Items: Item1(w=10, v=60), Item2(w=20, v=100),            │
│         Item3(w=30, v=120)                                 │
│  Knapsack capacity: W = 50                                 │
│                                                             │
│  Step 1: Calculate value-to-weight ratios                  │
│  Item1: 60/10 = 6.0                                       │
│  Item2: 100/20 = 5.0                                      │
│  Item3: 120/30 = 4.0                                      │
│                                                             │
│  Step 2: Sort by ratio (descending)                       │
│  Sorted order: Item1(6.0), Item2(5.0), Item3(4.0)        │
│                                                             │
│  Step 3: Fill knapsack greedily                           │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                KNAPSACK FILLING                         │ │
│  │                                                         │ │
│  │  Take Item1 completely:                                 │ │
│  │  • Weight used: 10, Value gained: 60                   │ │
│  │  • Remaining capacity: 50 - 10 = 40                    │ │
│  │                                                         │ │
│  │  Take Item2 completely:                                 │ │
│  │  • Weight used: 20, Value gained: 100                  │ │
│  │  • Remaining capacity: 40 - 20 = 20                    │ │
│  │                                                         │ │
│  │  Take Item3 partially:                                  │ │
│  │  • Available capacity: 20, Item3 weight: 30            │ │
│  │  • Fraction: 20/30 = 2/3                               │ │
│  │  • Value gained: (2/3) × 120 = 80                      │ │
│  │  • Remaining capacity: 0                               │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Final Result:                                             │
│  • Total value: 60 + 100 + 80 = 240                       │
│  • Items taken: Item1(100%), Item2(100%), Item3(66.67%)   │
│                                                             │
│  Verification:                                             │
│  • Total weight: 10 + 20 + (2/3)×30 = 10 + 20 + 20 = 50  │ │
│  • Capacity constraint satisfied ✓                         │
└─────────────────────────────────────────────────────────────┘
```

## 6. Job Sequencing with Deadlines

### Problem Statement
```
┌─────────────────────────────────────────────────────────────┐
│             JOB SEQUENCING WITH DEADLINES                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Problem: Given n jobs with deadlines and profits,         │
│  schedule jobs to maximize profit such that each job       │
│  is completed before its deadline                          │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    CONSTRAINTS                          │ │
│  │                                                         │ │
│  │  • Each job takes exactly 1 unit of time               │ │
│  │  • Only one job can be processed at a time             │ │
│  │  • Job must be completed before its deadline           │ │
│  │  • Each job can be scheduled at most once              │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Input: Jobs with (JobID, Deadline, Profit)               │
│  Output: Maximum profit and job sequence                   │
│                                                             │
│  Example Input:                                            │
│  Job1: (1, 4, 20), Job2: (2, 1, 10), Job3: (3, 1, 40),   │
│  Job4: (4, 1, 30)                                         │
└─────────────────────────────────────────────────────────────┘
```

### Greedy Strategy
```
┌─────────────────────────────────────────────────────────────┐
│                 GREEDY APPROACH                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Strategy: Sort jobs by profit in descending order,        │
│  then schedule each job at the latest possible time        │
│  before its deadline                                        │
│                                                             │
│  Algorithm: JobSequencing(jobs[], n)                       │
│  {                                                          │
│      // Sort jobs by profit (descending)                   │
│      sort jobs by profit (descending)                      │
│                                                             │
│      // Find maximum deadline                              │
│      maxDeadline = max(job.deadline for all jobs)          │
│                                                             │
│      // Initialize schedule array                          │
│      schedule[1..maxDeadline] = -1  // -1 means free       │
│                                                             │
│      totalProfit = 0                                       │
│      selectedJobs = []                                     │
│                                                             │
│      for each job in sorted order {                        │
│          // Try to schedule at latest possible time        │
│          for (time = min(job.deadline, maxDeadline);       │
│               time >= 1; time--) {                         │
│              if (schedule[time] == -1) {                   │
│                  schedule[time] = job.id                   │
│                  totalProfit += job.profit                 │
│                  selectedJobs.add(job)                     │
│                  break                                      │
│              }                                              │
│          }                                                  │
│      }                                                      │
│                                                             │
│      return (totalProfit, selectedJobs)                    │
│  }                                                          │
│                                                             │
│  │  Time Complexity: O(n²)                                   │
│  │  Space Complexity: O(max_deadline)                        │
└─────────────────────────────────────────────────────────────┘
```

### Job Sequencing Example
```
┌─────────────────────────────────────────────────────────────┐
│             JOB SEQUENCING EXAMPLE                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Input Jobs:                                               │
│  Job1: (ID=1, Deadline=4, Profit=20)                      │
│  Job2: (ID=2, Deadline=1, Profit=10)                      │
│  Job3: (ID=3, Deadline=1, Profit=40)                      │
│  Job4: (ID=4, Deadline=1, Profit=30)                      │
│                                                             │
│  Step 1: Sort by profit (descending)                      │
│  Sorted: Job3(40), Job4(30), Job1(20), Job2(10)           │
│                                                             │
│  Step 2: Initialize schedule array                        │
│  Max deadline = 4                                         │
│  Schedule: [-, -, -, -] (time slots 1, 2, 3, 4)           │
│                                                             │
│  Step 3: Schedule jobs greedily                           │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                SCHEDULING PROCESS                       │ │
│  │                                                         │ │
│  │  Process Job3 (deadline=1, profit=40):                 │ │
│  │  • Try time slot 1: Available ✓                       │ │
│  │  • Schedule Job3 at time 1                             │ │
│  │  • Schedule: [3, -, -, -]                              │ │
│  │  • Total profit: 40                                    │ │
│  │                                                         │ │
│  │  Process Job4 (deadline=1, profit=30):                 │ │
│  │  • Try time slot 1: Occupied ✗                        │ │
│  │  • Job4 cannot be scheduled (missed deadline)          │ │
│  │  • Schedule: [3, -, -, -]                              │ │
│  │  • Total profit: 40                                    │ │
│  │                                                         │ │
│  │  Process Job1 (deadline=4, profit=20):                 │ │
│  │  • Try time slot 4: Available ✓                       │ │
│  │  • Schedule Job1 at time 4                             │ │
│  │  • Schedule: [3, -, -, 1]                              │ │
│  │  • Total profit: 40 + 20 = 60                          │ │
│  │                                                         │ │
│  │  Process Job2 (deadline=1, profit=10):                 │ │
│  │  • Try time slot 1: Occupied ✗                        │ │
│  │  • Job2 cannot be scheduled (missed deadline)          │ │
│  │  • Schedule: [3, -, -, 1]                              │ │
│  │  • Total profit: 60                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Final Result:                                             │
│  • Selected jobs: Job3, Job1                              │
│  • Job sequence: Job3 → Job1                              │
│  • Maximum profit: 60                                     │
│  • Time utilization: 2 out of 4 time slots               │
└─────────────────────────────────────────────────────────────┘
```

## 7. Single Source Shortest Path (Dijkstra's Algorithm)

### Problem Statement
```
┌─────────────────────────────────────────────────────────────┐
│            SINGLE SOURCE SHORTEST PATH                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Problem: Given a weighted graph and a source vertex,      │
│  find the shortest path from source to all other vertices  │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  ASSUMPTIONS                            │ │
│  │                                                         │ │
│  │  • Graph can be directed or undirected                 │ │
│  │  • All edge weights are non-negative                   │ │
│  │  • Graph is connected                                  │ │
│  │  • No negative cycles                                  │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Input: Graph G(V,E), source vertex s                     │
│  Output: Shortest distance from s to all vertices         │
│                                                             │
│  Applications:                                             │
│  • GPS navigation systems                                  │
│  • Network routing protocols                              │
│  • Social networks (degrees of separation)                │
│  • Game AI (pathfinding)                                  │
└─────────────────────────────────────────────────────────────┘
```

### Dijkstra's Algorithm
```
┌─────────────────────────────────────────────────────────────┐
│                DIJKSTRA'S ALGORITHM                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Strategy: Maintain a set of vertices whose shortest       │
│  distance is known, and greedily add the closest vertex    │
│                                                             │
│  Algorithm: Dijkstra(Graph G, source s)                    │
│  {                                                          │
│      // Initialize distances                               │
│      for each vertex v in V {                              │
│          distance[v] = ∞                                   │
│          previous[v] = null                                │
│      }                                                      │
│      distance[s] = 0                                       │
│                                                             │
│      // Initialize priority queue                          │
│      PriorityQueue pq                                      │
│      for each vertex v in V {                              │
│          pq.insert(v, distance[v])                         │
│      }                                                      │
│                                                             │
│      while (pq is not empty) {                             │
│          u = pq.extractMin()                               │
│                                                             │
│          // Relax all edges from u                         │
│          for each neighbor v of u {                        │
│              alt = distance[u] + weight(u,v)               │
│              if (alt < distance[v]) {                      │
│                  distance[v] = alt                         │
│                  previous[v] = u                           │
│                  pq.decreaseKey(v, alt)                    │
│              }                                              │
│          }                                                  │
│      }                                                      │
│      return distance[], previous[]                         │
│  }                                                          │
│                                                             │
│  Time Complexity: O((V + E) log V) with binary heap       │
│  Space Complexity: O(V)                                   │
└─────────────────────────────────────────────────────────────┘
```

### Dijkstra Example
```
┌─────────────────────────────────────────────────────────────┐
│               DIJKSTRA'S ALGORITHM EXAMPLE                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Input Graph (Source: A):                                 │
│                                                             │
│      A ------4------ B ------8------ C                     │
│      |\\             |               |                     │
│      | \\           |               |                      │
│      |  8\\         |7              |4                     │
│      |    \\        |               |                      │
│      |     \\       |               |                      │
│      2       \\     |               |                      │
│      |         \\   |               |                      │
│      |          \\  |               |                      │
│      |           \\ |               |                      │
│      D ------9------ E ------10----- F                     │
│                      |                                     │
│                     |2                                     │
│                      |                                     │
│                      H                                     │
│                                                             │
│  Step-by-step execution:                                   │
│                                                             │
│  Initial state:                                            │
│  distance[A]=0, all others=∞                              │
│  PQ: A(0), B(∞), C(∞), D(∞), E(∞), F(∞), H(∞)            │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  ITERATION DETAILS                      │ │
│  │                                                         │ │
│  │  Extract A(0):                                         │ │
│  │  • Relax A→B: distance[B] = min(∞, 0+4) = 4           │ │
│  │  • Relax A→D: distance[D] = min(∞, 0+2) = 2           │ │
│  │  • Relax A→E: distance[E] = min(∞, 0+8) = 8           │ │
│  │  PQ: D(2), B(4), E(8), C(∞), F(∞), H(∞)               │ │
│  │                                                         │ │
│  │  Extract D(2):                                         │ │
│  │  • Relax D→E: distance[E] = min(8, 2+9) = 8 (no change)│ │
│  │  PQ: B(4), E(8), C(∞), F(∞), H(∞)                     │ │
│  │                                                         │ │
│  │  Extract B(4):                                         │ │
│  │  • Relax B→C: distance[C] = min(∞, 4+8) = 12          │ │
│  │  • Relax B→E: distance[E] = min(8, 4+7) = 7           │ │
│  │  PQ: E(7), C(12), F(∞), H(∞)                          │ │
│  │                                                         │ │
│  │  Extract E(7):                                         │ │
│  │  • Relax E→F: distance[F] = min(∞, 7+10) = 17         │ │
│  │  • Relax E→H: distance[H] = min(∞, 7+2) = 9           │ │
│  │  PQ: H(9), C(12), F(17)                               │ │
│  │                                                         │ │
│  │  Extract H(9), C(12), F(17) in order...               │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Final shortest distances from A:                         │
│  • A: 0                                                   │
│  • B: 4  (path: A → B)                                    │
│  • C: 12 (path: A → B → C)                                │
│  • D: 2  (path: A → D)                                    │
│  • E: 7  (path: A → B → E)                                │
│  • F: 17 (path: A → B → E → F)                            │
│  • H: 9  (path: A → B → E → H)                            │
└─────────────────────────────────────────────────────────────┘
```

## 8. Algorithm Comparison and Analysis

### Greedy Algorithms Summary
```
┌─────────────────────────────────────────────────────────────┐
│                GREEDY ALGORITHMS COMPARISON                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┬──────────────┬──────────────┬──────────────┐ │
│  │  Algorithm  │ Time Complexity │ Space Complexity │ Optimal? │ │
│  ├─────────────┼──────────────┼──────────────┼──────────────┤ │
│  │ Optimal     │ O(n log n)   │ O(n)         │ Yes          │ │
│  │ Merge       │              │              │              │ │
│  ├─────────────┼──────────────┼──────────────┼──────────────┤ │
│  │ Huffman     │ O(n log n)   │ O(n)         │ Yes          │ │
│  │ Coding      │              │              │              │ │
│  ├─────────────┼──────────────┼──────────────┼──────────────┤ │
│  │ Kruskal's   │ O(E log E)   │ O(V)         │ Yes          │ │
│  │ MST         │              │              │              │ │
│  ├─────────────┼──────────────┼──────────────┼──────────────┤ │
│  │ Prim's MST  │ O(E log V)   │ O(V)         │ Yes          │ │
│  │             │              │              │              │ │
│  ├─────────────┼──────────────┼──────────────┼──────────────┤ │
│  │ Fractional  │ O(n log n)   │ O(1)         │ Yes          │ │
│  │ Knapsack    │              │              │              │ │
│  ├─────────────┼──────────────┼──────────────┼──────────────┤ │
│  │ Job         │ O(n²)        │ O(n)         │ Yes          │ │
│  │ Sequencing  │              │              │              │ │
│  ├─────────────┼──────────────┼──────────────┼──────────────┤ │
│  │ Dijkstra's  │ O((V+E)log V)│ O(V)         │ Yes*         │ │
│  │ SSSP        │              │              │ (non-neg)    │ │
│  └─────────────┴──────────────┴──────────────┴──────────────┘ │
│                                                             │
│  Key Observations:                                         │
│  • Most greedy algorithms have O(n log n) complexity       │
│  • Space complexity is usually O(n) or better             │
│  • Greedy approach gives optimal solution for these        │
│  • Performance depends on data structure choice            │
└─────────────────────────────────────────────────────────────┘
```

### When to Use Greedy vs Other Approaches
```
┌─────────────────────────────────────────────────────────────┐
│                 STRATEGY SELECTION GUIDE                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   USE GREEDY WHEN:                      │ │
│  │                                                         │ │
│  │  ✓ Problem has greedy choice property                   │ │
│  │  ✓ Problem has optimal substructure                     │ │
│  │  ✓ Local optimum leads to global optimum               │ │
│  │  ✓ Need fast, simple solution                          │ │
│  │  ✓ Problem fits known greedy patterns                  │ │
│  │                                                         │ │
│  │  Examples: MST, shortest path, activity selection,     │ │
│  │  fractional knapsack, Huffman coding                   │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                USE DYNAMIC PROGRAMMING:                 │ │
│  │                                                         │ │
│  │  ✓ Optimal substructure present                        │ │
│  │  ✓ Overlapping subproblems                             │ │
│  │  ✓ Greedy doesn't work (0/1 knapsack)                  │ │
│  │  ✓ Need to consider all possibilities                  │ │
│  │                                                         │ │
│  │  Examples: 0/1 knapsack, longest common subsequence,   │ │
│  │  edit distance, coin change (certain cases)            │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 USE DIVIDE & CONQUER:                   │ │
│  │                                                         │ │
│  │  ✓ Problem can be broken into subproblems              │ │
│  │  ✓ Subproblems are independent                         │ │
│  │  ✓ Combine step is straightforward                     │ │
│  │                                                         │ │
│  │  Examples: merge sort, quick sort, binary search,      │ │
│  │  closest pair, maximum subarray                        │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Common Pitfalls and Tips
```
┌─────────────────────────────────────────────────────────────┐
│                 COMMON PITFALLS & TIPS                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    PITFALLS                             │ │
│  │                                                         │ │
│  │  ❌ Assuming greedy always works                        │ │
│  │     Counter-example: 0/1 knapsack                      │ │
│  │                                                         │ │
│  │  ❌ Wrong greedy choice criterion                       │ │
│  │     Example: In fractional knapsack, choosing by       │ │
│  │     value alone instead of value/weight ratio          │ │
│  │                                                         │ │
│  │  ❌ Not proving correctness                             │ │
│  │     Must show greedy choice property and optimal       │ │
│  │     substructure                                        │ │
│  │                                                         │ │
│  │  ❌ Inefficient data structure choice                   │ │
│  │     Using array instead of heap for priority queue     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                      TIPS                               │ │
│  │                                                         │ │
│  │  ✓ Always verify greedy choice property                │ │
│  │  ✓ Use appropriate data structures (heaps, union-find) │ │
│  │  ✓ Sort data when needed for greedy choice             │ │
│  │  ✓ Consider edge cases (empty input, single element)   │ │
│  │  ✓ Trace through small examples to verify logic        │ │
│  │  ✓ Compare with brute force on small inputs            │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 9. Quick Revision

### Must Remember Formulas and Concepts
```
┌─────────────────────────────────────────────────────────────┐
│                    QUICK REFERENCE                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                KEY CONCEPTS                             │ │
│  │                                                         │ │
│  │  Greedy Choice Property:                               │ │
│  │  A globally optimal solution can be reached by making  │ │
│  │  locally optimal choices                               │ │
│  │                                                         │ │
│  │  Optimal Substructure:                                │ │
│  │  An optimal solution contains optimal solutions to     │ │
│  │  subproblems                                           │ │
│  │                                                         │ │
│  │  Fractional Knapsack Ratio:                           │ │
│  │  Sort by value/weight ratio in descending order       │ │
│  │                                                         │ │
│  │  MST Properties:                                       │ │
│  │  • Exactly V-1 edges for V vertices                   │ │
│  │  • Connected, acyclic                                 │ │
│  │  • Minimum total edge weight                          │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                TIME COMPLEXITIES                        │ │
│  │                                                         │ │
│  │  Optimal Merge: O(n log n)                            │ │
│  │  Huffman Coding: O(n log n)                           │ │
│  │  Kruskal's MST: O(E log E)                            │ │
│  │  Prim's MST: O(E log V) or O(E + V log V)             │ │
│  │  Fractional Knapsack: O(n log n)                      │ │
│  │  Job Sequencing: O(n²)                                │ │
│  │  Dijkstra's SSSP: O((V+E) log V)                      │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Important Questions and Problem Types
```
┌─────────────────────────────────────────────────────────────┐
│                   EXAM PREPARATION                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              COMMON QUESTION TYPES                      │ │
│  │                                                         │ │
│  │  1. Algorithm Trace Questions:                         │ │
│  │     • Trace Huffman coding step-by-step               │ │
│  │     • Execute Kruskal's/Prim's on given graph         │ │
│  │     • Show Dijkstra's algorithm execution             │ │
│  │                                                         │ │
│  │  2. Optimization Problems:                             │ │
│  │     • Find minimum merge cost                          │ │
│  │     • Maximize profit in job sequencing               │ │
│  │     • Optimal knapsack filling                        │ │
│  │                                                         │ │
│  │  3. Proof Questions:                                   │ │
│  │     • Prove greedy choice property                     │ │
│  │     • Show optimal substructure                       │ │
│  │     • Compare greedy vs dynamic programming           │ │
│  │                                                         │ │
│  │  4. Complexity Analysis:                               │ │
│  │     • Time and space complexity derivation            │ │
│  │     • Compare different algorithm approaches           │ │
│  │     • Best/average/worst case analysis                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    STUDY TIPS                           │ │
│  │                                                         │ │
│  │  • Practice tracing algorithms with different inputs   │ │
│  │  • Understand why greedy works for each problem        │ │
│  │  • Memorize key data structures (heap, union-find)     │ │
│  │  • Know when greedy fails (0/1 knapsack)              │ │
│  │  • Practice complexity analysis                        │ │
│  │  • Understand real-world applications                  │ │
│  │  • Compare different algorithms for same problem       │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Final Checklist
```
┌─────────────────────────────────────────────────────────────┐
│                    FINAL CHECKLIST                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Before the exam, make sure you can:                       │
│                                                             │
│  □ Define greedy strategy and its properties               │
│  □ Trace optimal merge patterns algorithm                  │
│  □ Build Huffman tree and calculate codes                  │
│  □ Execute Kruskal's and Prim's MST algorithms             │
│  □ Solve fractional knapsack problems                      │
│  □ Schedule jobs with deadlines optimally                  │
│  □ Run Dijkstra's shortest path algorithm                  │
│  □ Analyze time and space complexity                       │
│  □ Compare greedy with other paradigms                     │
│  □ Identify when greedy approach works                     │
│                                                             │
│  Key takeaway: Greedy algorithms make locally optimal      │
│  choices hoping to achieve global optimum. They work       │
│  when problem has greedy choice property and optimal       │
│  substructure.                                             │
└─────────────────────────────────────────────────────────────┘
```

---

**End of Unit II: Greedy Strategy and Algorithms**

*This comprehensive coverage includes all syllabus topics with detailed explanations, examples, and exam preparation material.*



