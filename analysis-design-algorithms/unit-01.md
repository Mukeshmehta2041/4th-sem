# Unit I: Analysis and Design of Algorithms

## 0. Syllabus
Algorithms, Designing algorithms, analyzing algorithms, asymptotic notations, heap and heap sort. Introduction to divide and conquer technique, analysis, design and comparison of various algorithms based on this technique, example binary search, merge sort, quick sort, strassen's matrix multiplication.

## 1. Introduction to Algorithms

### What is an Algorithm?
```
┌─────────────────────────────────────────────────────────────┐
│                    ALGORITHM                                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                     INPUT                               │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Data 1    │  │   Data 2    │  │   Data n    │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           │                                │
│                           ▼                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   ALGORITHM                             │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │   Step 1    │→ │   Step 2    │→ │   Step n    │     │ │
│  │  │  (Finite)   │  │  (Definite) │  │ (Effective) │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           │                                │
│                           ▼                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    OUTPUT                               │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │ │
│  │  │  Result 1   │  │  Result 2   │  │  Result m   │     │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

**Definition**: An algorithm is a step-by-step procedure for solving a problem or completing a task in a finite number of steps.

### Properties of Algorithms
```
┌─────────────────────────────────────────────────────────────┐
│                ALGORITHM PROPERTIES                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │  Finiteness │  │  Definiteness│ │ Effectiveness│         │
│  │             │  │             │  │             │         │
│  │ • Must      │  │ • Each step │  │ • Operations│         │
│  │   terminate │  │   clearly   │  │   are basic │         │
│  │ • Finite    │  │ • No        │  │   performed │         │
│  │   steps     │  │   ambiguity │  │   exactly   │         │
│  │             │  │   defined   │  │ • Can be    │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │    Input    │  │   Output    │                          │
│  │             │  │             │                          │
│  │ • Zero or   │  │ • At least  │                          │
│  │   more      │  │   one       │                          │
│  │   inputs    │  │   output    │                          │
│  │ • Well      │  │ • Desired   │                          │
│  │   defined   │  │   relation  │                          │
│  └─────────────┘  └─────────────┘                          │
└─────────────────────────────────────────────────────────────┘
```

**Properties Explained:**
1. **Finiteness**: Algorithm must terminate after finite number of steps
2. **Definiteness**: Each step must be precisely defined
3. **Input**: Zero or more well-defined inputs
4. **Output**: At least one output with desired relation to inputs
5. **Effectiveness**: Operations must be basic and executable

### Algorithm vs Program
```
┌─────────────────────────────────────────────────────────────┐
│              ALGORITHM vs PROGRAM                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   ALGORITHM                             │ │
│  │                                                         │ │
│  │  • Step-by-step procedure                               │ │
│  │  • Language independent                                 │ │
│  │  • Design phase                                         │ │
│  │  • Mathematical concept                                 │ │
│  │  • Problem-solving logic                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           │                                │
│                           ▼                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    PROGRAM                              │ │
│  │                                                         │ │
│  │  • Implementation of algorithm                          │ │
│  │  • Language dependent                                   │ │
│  │  • Implementation phase                                 │ │
│  │  • Code written in specific language                    │ │
│  │  • Executable on computer                               │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 2. Designing Algorithms

### Algorithm Design Process
```
┌─────────────────────────────────────────────────────────────┐
│                ALGORITHM DESIGN PROCESS                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │ Problem     │───▶│ Algorithm   │───▶│ Analysis    │     │
│  │ Definition  │    │ Design      │    │             │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │• Understand │    │• Choose     │    │• Time       │     │
│  │  problem    │    │  technique  │    │  complexity │     │
│  │• Define     │    │• Write      │    │• Space      │     │
│  │  inputs     │    │  pseudocode │    │  complexity │     │
│  │• Define     │    │• Verify     │    │• Correctness│     │
│  │  outputs    │    │  correctness│    │  proof      │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
│                          │                                 │
│                          ▼                                 │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 IMPLEMENTATION                          │ │
│  │                                                         │ │
│  │  • Code in programming language                         │ │
│  │  • Testing and debugging                                │ │
│  │  • Optimization                                         │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Algorithm Design Techniques
```
┌─────────────────────────────────────────────────────────────┐
│              ALGORITHM DESIGN TECHNIQUES                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Brute     │  │   Divide    │  │   Greedy    │         │
│  │   Force     │  │    and      │  │             │         │
│  │             │  │  Conquer    │  │             │         │
│  │ • Try all   │  │ • Break     │  │ • Local     │         │
│  │   solutions │  │   problem   │  │   optimal   │         │
│  │ • Simple    │  │ • Solve     │  │ • Quick     │         │
│  │ • Slow      │  │   parts     │  │   decisions │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │  Dynamic    │  │  Backtrack  │  │  Branch     │         │
│  │ Programming │  │             │  │    and      │         │
│  │             │  │             │  │   Bound     │         │
│  │ • Optimal   │  │ • Try and   │  │   tree      │         │
│  │   subprob   │  │   undo      │  │ • Pruning   │         │
│  │ • Memoize   │  │ • Systematic│  │ • Optimal   │         │
│  │ • Efficient │  │   search    │  │ • Optimal   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

### Example: Finding Maximum Element
```
Algorithm: FindMax(A[1..n])
Input: Array A of n elements
Output: Maximum element in array

1. max ← A[1]                    // Initialize with first element
2. for i ← 2 to n do            // Check remaining elements
3.     if A[i] > max then       // If current element is larger
4.         max ← A[i]           // Update maximum
5. return max                    // Return the maximum

Time Complexity: O(n)
Space Complexity: O(1)
```

## 3. Analyzing Algorithms

### Why Algorithm Analysis?
```
┌─────────────────────────────────────────────────────────────┐
│                 WHY ANALYZE ALGORITHMS?                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 PERFORMANCE                             │ │
│  │                                                         │ │
│  │  • Predict running time                                 │ │
│  │  • Compare different algorithms                         │ │
│  │  • Identify bottlenecks                                 │ │
│  │  • Optimize resource usage                              │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  SCALABILITY                            │ │
│  │                                                         │ │
│  │  • How algorithm behaves with large inputs              │ │
│  │  • Memory requirements                                  │ │
│  │  • Feasibility for real-world applications             │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 CORRECTNESS                             │ │
│  │                                                         │ │
│  │  • Verify algorithm produces correct output             │ │
│  │  • Handle edge cases                                    │ │
│  │  • Prove algorithm terminates                           │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Types of Analysis
```
┌─────────────────────────────────────────────────────────────┐
│                   TYPES OF ANALYSIS                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Best      │  │   Average   │  │   Worst     │         │
│  │   Case      │  │    Case     │  │   Case      │         │
│  │             │  │             │  │             │         │
│  │ • Minimum   │  │ • Expected  │  │ • Maximum   │         │
│  │   time      │  │   time      │  │   time      │         │
│  │ • Optimal   │  │ • Typical   │  │ • Pessimistic│         │
│  │   input     │  │   input     │  │   input     │         │
│  │ • Lower     │  │ • Realistic │  │ • Upper     │         │
│  │   bound     │  │   scenario  │  │   bound     │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│        Ω(f(n))          Θ(f(n))          O(f(n))           │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Different scenarios for algorithm performance              │
└─────────────────────────────────────────────────────────────┘
```

### Time and Space Complexity
```
┌─────────────────────────────────────────────────────────────┐
│              TIME AND SPACE COMPLEXITY                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                TIME COMPLEXITY                          │ │
│  │                                                         │ │
│  │  • Amount of time algorithm takes to run                │ │
│  │  • Function of input size (n)                           │ │
│  │  • Count primitive operations                           │ │
│  │  • Independent of hardware/software                     │ │
│  │                                                         │ │
│  │  Examples:                                              │ │
│  │  • T(n) = 5n + 3        → O(n)                          │ │
│  │  • T(n) = 2n² + n + 1   → O(n²)                         │ │
│  │  • T(n) = log₂n + 5     → O(log n)                      │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                SPACE COMPLEXITY                         │ │
│  │                                                         │ │
│  │  • Amount of memory algorithm uses                      │ │
│  │  • Function of input size (n)                           │ │
│  │  • Includes auxiliary space                             │ │
│  │  • Excludes input space (sometimes)                     │ │
│  │                                                         │ │
│  │  Examples:                                              │ │
│  │  • S(n) = 5             → O(1)                          │ │
│  │  • S(n) = 2n            → O(n)                          │ │
│  │  • S(n) = n² + n        → O(n²)                         │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 4. Asymptotic Notations

### What are Asymptotic Notations?
```
┌─────────────────────────────────────────────────────────────┐
│               ASYMPTOTIC NOTATIONS                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Mathematical tools to describe the running time of        │
│  algorithms as the input size approaches infinity          │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │Big O (O)    │  │Big Omega(Ω)│  │Big Theta(Θ) │         │
│  │             │  │             │  │             │         │
│  │Upper Bound  │  │Lower Bound  │  │Tight Bound  │         │
│  │Worst Case   │  │Best Case    │  │Average Case │         │
│  │≤ f(n)       │  │≥ f(n)       │  │= f(n)       │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  Focus on growth rate, ignore constants and lower terms    │
│  Example: 3n² + 2n + 1 → O(n²)                            │
└─────────────────────────────────────────────────────────────┘
```

### Big O Notation (O)
```
┌─────────────────────────────────────────────────────────────┐
│                    BIG O NOTATION                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Definition: f(n) = O(g(n)) if there exist positive       │
│  constants c and n₀ such that:                             │
│                                                             │
│            f(n) ≤ c × g(n) for all n ≥ n₀                  │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    GRAPH                                │ │
│  │   f(n)                                                  │ │
│  │     ▲                                                   │ │
│  │     │     c×g(n) ___________________                     │ │
│  │     │           /                                       │ │
│  │     │     f(n) /                                        │ │
│  │     │         /                                         │ │
│  │     │   _____/                                          │ │
│  │     │  /                                                │ │
│  │     │ /                                                 │ │
│  │     └──────────────────────────────────▶ n              │ │
│  │       n₀                                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Properties:                                               │
│  • Upper bound (worst-case)                                │
│  • Describes maximum growth rate                           │
│  • Most commonly used notation                             │
│                                                             │
│  Examples:                                                 │
│  • 5n + 3 = O(n)                                          │
│  • n² + 100n = O(n²)                                      │
│  • log n + 5 = O(log n)                                   │
└─────────────────────────────────────────────────────────────┘
```

### Big Omega Notation (Ω)
```
┌─────────────────────────────────────────────────────────────┐
│                  BIG OMEGA NOTATION                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Definition: f(n) = Ω(g(n)) if there exist positive       │
│  constants c and n₀ such that:                             │
│                                                             │
│            f(n) ≥ c × g(n) for all n ≥ n₀                  │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    GRAPH                                │ │
│  │   f(n)                                                  │ │
│  │     ▲                                                   │ │
│  │     │                                                   │ │
│  │     │     f(n) ___________________                       │ │
│  │     │         /                                         │ │
│  │     │        /                                          │ │
│  │     │       /                                           │ │
│  │     │   c×g(n)                                          │ │
│  │     │     /                                             │ │
│  │     │    /                                              │ │
│  │     └──────────────────────────────────▶ n              │ │
│  │       n₀                                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Properties:                                               │
│  • Lower bound (best-case)                                 │
│  • Describes minimum growth rate                           │
│  • Less commonly used than Big O                           │
│                                                             │
│  Examples:                                                 │
│  • n² + n = Ω(n²)                                         │
│  • 5n + 100 = Ω(n)                                        │
│  • n log n = Ω(n log n)                                   │
└─────────────────────────────────────────────────────────────┘
```

### Big Theta Notation (Θ)
```
┌─────────────────────────────────────────────────────────────┐
│                  BIG THETA NOTATION                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Definition: f(n) = Θ(g(n)) if there exist positive       │
│  constants c₁, c₂ and n₀ such that:                        │
│                                                             │
│        c₁ × g(n) ≤ f(n) ≤ c₂ × g(n) for all n ≥ n₀        │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    GRAPH                                │ │
│  │   f(n)                                                  │ │
│  │     ▲                                                   │ │
│  │     │   c₂×g(n) ___________________                      │ │
│  │     │           /                                       │ │
│  │     │     f(n) /                                        │ │
│  │     │         /                                         │ │
│  │     │   c₁×g(n)                                         │ │
│  │     │       /                                           │ │
│  │     │      /                                            │ │
│  │     └──────────────────────────────────▶ n              │ │
│  │       n₀                                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Properties:                                               │
│  • Tight bound (average-case)                              │
│  • Exact growth rate                                       │
│  • f(n) = Θ(g(n)) iff f(n) = O(g(n)) AND f(n) = Ω(g(n))  │
│                                                             │
│  Examples:                                                 │
│  • 3n + 5 = Θ(n)                                          │
│  • n² + 2n + 1 = Θ(n²)                                    │
│  • n log n + n = Θ(n log n)                               │
└─────────────────────────────────────────────────────────────┘
```

### Common Growth Rates
```
┌─────────────────────────────────────────────────────────────┐
│                 COMMON GROWTH RATES                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  From Fastest to Slowest:                                  │
│                                                             │
│  O(1)        → Constant         → Hash table access        │
│  O(log n)    → Logarithmic      → Binary search            │
│  O(n)        → Linear           → Array traversal          │
│  O(n log n)  → Linearithmic     → Merge sort               │
│  O(n²)       → Quadratic        → Bubble sort              │
│  O(n³)       → Cubic            → Matrix multiplication    │
│  O(2ⁿ)       → Exponential      → Brute force subsets     │
│  O(n!)       → Factorial        → Traveling salesman      │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 GROWTH COMPARISON                       │ │
│  │                                                         │ │
│  │  Time                                                   │ │
│  │   ▲                                                     │ │
│  │   │                                          O(n!)      │ │
│  │   │                                    O(2ⁿ)           │ │
│  │   │                             O(n³)                  │ │
│  │   │                      O(n²)                         │ │
│  │   │               O(n log n)                           │ │
│  │   │         O(n)                                       │ │
│  │   │   O(log n)                                         │ │
│  │   │ O(1)_____                                          │ │
│  │   └──────────────────────────────────────▶ n           │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Rules for Asymptotic Analysis
```
┌─────────────────────────────────────────────────────────────┐
│              RULES FOR ASYMPTOTIC ANALYSIS                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. CONSTANTS: Ignore constant factors                     │
│     • 5n = O(n), not O(5n)                                │
│     • 100 = O(1), not O(100)                              │
│                                                             │
│  2. LOWER ORDER TERMS: Drop lower order terms              │
│     • n² + n = O(n²), not O(n² + n)                       │
│     • n³ + n² + n + 1 = O(n³)                             │
│                                                             │
│  3. LOOPS:                                                 │
│     • Single loop: O(n)                                   │
│     • Nested loops: O(n²), O(n³), etc.                   │
│     • Sequential loops: O(n + m) = O(max(n,m))            │
│                                                             │
│  4. RECURSION: Use recurrence relations                    │
│     • T(n) = T(n/2) + O(1) → O(log n)                     │
│     • T(n) = 2T(n/2) + O(n) → O(n log n)                  │
│                                                             │
│  5. CONDITIONAL STATEMENTS:                                │
│     • Take the worst case complexity                       │
│     • if-else: O(max(if_part, else_part))                 │
└─────────────────────────────────────────────────────────────┘
```

### Examples of Complexity Analysis
```
Example 1: Simple Loop
for i = 1 to n do
    print(A[i])

Analysis: Loop runs n times, each iteration is O(1)
Time Complexity: O(n)
Space Complexity: O(1)

Example 2: Nested Loop
for i = 1 to n do
    for j = 1 to n do
        print(A[i] + A[j])

Analysis: Outer loop runs n times, inner loop runs n times
Time Complexity: O(n²)
Space Complexity: O(1)

Example 3: Logarithmic
while n > 1 do
    n = n / 2

Analysis: n is halved each iteration
Number of iterations: log₂(n)
Time Complexity: O(log n)
Space Complexity: O(1)
```

## 5. Heap and Heap Sort

### What is a Heap?
```
┌─────────────────────────────────────────────────────────────┐
│                       HEAP                                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  A complete binary tree that satisfies the heap property   │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  HEAP PROPERTY                          │ │
│  │                                                         │ │
│  │  Max Heap: Parent ≥ Children                            │ │
│  │  Min Heap: Parent ≤ Children                            │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 COMPLETE BINARY TREE                    │ │
│  │                                                         │ │
│  │  • All levels filled except possibly the last          │ │
│  │  • Last level filled from left to right                │ │
│  │  • Can be represented as an array                       │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Max Heap Example
```
┌─────────────────────────────────────────────────────────────┐
│                    MAX HEAP EXAMPLE                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                        100                                  │
│                      /     \                               │
│                    90       80                             │
│                   /  \     /  \                            │
│                  70   60  50   40                          │
│                 / \                                        │
│                30  20                                      │
│                                                             │
│  Array Representation:                                     │
│  Index:  0   1   2   3   4   5   6   7   8                 │
│  Value: 100  90  80  70  60  50  40  30  20                │
│                                                             │
│  Relationships:                                            │
│  • Parent(i) = (i-1)/2                                    │
│  • Left child(i) = 2*i + 1                                │
│  • Right child(i) = 2*i + 2                               │
│                                                             │
│  Properties:                                               │
│  • Root has maximum value                                  │
│  • Every parent ≥ its children                            │
│  • Height = O(log n)                                      │
└─────────────────────────────────────────────────────────────┘
```

### Min Heap Example
```
┌─────────────────────────────────────────────────────────────┐
│                    MIN HEAP EXAMPLE                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                         10                                  │
│                      /     \                               │
│                    20       30                             │
│                   /  \     /  \                            │
│                  40   50  60   70                          │
│                 / \                                        │
│                80  90                                      │
│                                                             │
│  Array Representation:                                     │
│  Index:  0   1   2   3   4   5   6   7   8                 │
│  Value:  10  20  30  40  50  60  70  80  90                │
│                                                             │
│  Properties:                                               │
│  • Root has minimum value                                  │
│  • Every parent ≤ its children                            │
│  • Used in priority queues                                │
└─────────────────────────────────────────────────────────────┘
```

### Heap Operations

#### Insert Operation (Max Heap)
```
┌─────────────────────────────────────────────────────────────┐
│                  HEAP INSERT OPERATION                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Algorithm: Insert(heap, element)                          │
│  1. Add element at the end of heap                         │
│  2. Heapify up (bubble up) to maintain heap property       │
│                                                             │
│  Example: Insert 95 into max heap                          │
│                                                             │
│  Step 1: Insert at end                                     │
│                        100                                  │
│                      /     \                               │
│                    90       80                             │
│                   /  \     /  \                            │
│                  70   60  50   40                          │
│                 / \   /                                    │
│                30 20 95                                    │
│                                                             │
│  Step 2: Heapify up (95 > 60, so swap)                    │
│                        100                                  │
│                      /     \                               │
│                    90       80                             │
│                   /  \     /  \                            │
│                  70   95  50   40                          │
│                 / \   /                                    │
│                30 20 60                                    │
│                                                             │
│  Step 3: Heapify up (95 > 90, so swap)                    │
│                        100                                  │
│                      /     \                               │
│                    90       80                             │
│                   /  \     /  \                            │
│                  70   95  50   40                          │
│                 / \   /                                    │
│                30 20 60                                    │
│                                                             │
│  Time Complexity: O(log n)                                │
└─────────────────────────────────────────────────────────────┘
```

#### Delete Operation (Max Heap)
```
┌─────────────────────────────────────────────────────────────┐
│                 HEAP DELETE OPERATION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Algorithm: DeleteMax(heap)                                │
│  1. Replace root with last element                         │
│  2. Remove last element                                    │
│  3. Heapify down to maintain heap property                 │
│                                                             │
│  Example: Delete max from heap                             │
│                                                             │
│  Original:                                                 │
│                        100                                  │
│                      /     \                               │
│                    90       80                             │
│                   /  \     /  \                            │
│                  70   60  50   40                          │
│                 / \                                        │
│                30  20                                      │
│                                                             │
│  Step 1: Replace root with last element (20)              │
│                         20                                  │
│                      /     \                               │
│                    90       80                             │
│                   /  \     /  \                            │
│                  70   60  50   40                          │
│                 /                                          │
│                30                                          │
│                                                             │
│  Step 2: Heapify down (20 < 90, so swap with larger child)│
│                         90                                  │
│                      /     \                               │
│                    20       80                             │
│                   /  \     /  \                            │
│                  70   60  50   40                          │
│                 /                                          │
│                30                                          │
│                                                             │
│  Step 3: Continue heapify down (20 < 70, so swap)         │
│                         90                                  │
│                      /     \                               │
│                    70       80                             │
│                   /  \     /  \                            │
│                  20   60  50   40                          │
│                 /                                          │
│                30                                          │
│                                                             │
│  Step 4: Continue heapify down (20 < 30, so swap)         │
│                         90                                  │
│                      /     \                               │
│                    70       80                             │
│                   /  \     /  \                            │
│                  30   60  50   40                          │
│                 /                                          │
│                20                                          │
│                                                             │
│  Time Complexity: O(log n)                                │
└─────────────────────────────────────────────────────────────┘
```

### Heap Sort Algorithm
```
┌─────────────────────────────────────────────────────────────┐
│                    HEAP SORT ALGORITHM                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Algorithm: HeapSort(A[1..n])                              │
│  1. Build a max heap from input array                      │
│  2. For i = n down to 2:                                   │
│     a. Swap A[1] with A[i] (extract max)                   │
│     b. Decrease heap size by 1                             │
│     c. Heapify A[1] to maintain heap property              │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                     PROCESS                             │ │
│  │                                                         │ │
│  │  Phase 1: Build Max Heap                                │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │ Unsorted Array → Max Heap                           │ │ │
│  │  │ [4,1,3,2,16,9,10,14,8,7] → Build heap              │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  │                                                         │ │
│  │  Phase 2: Extract Maximum Elements                      │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │ Extract max → Place at end → Heapify                │ │ │
│  │  │ Repeat until sorted                                 │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Time Complexity: O(n log n)                              │
│  Space Complexity: O(1) - In-place sorting                │
│  Stability: Not stable                                     │
└─────────────────────────────────────────────────────────────┘
```

### Heap Sort Example
```
┌─────────────────────────────────────────────────────────────┐
│                   HEAP SORT EXAMPLE                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Input Array: [4, 1, 3, 2, 16, 9, 10, 14, 8, 7]          │
│                                                             │
│  Step 1: Build Max Heap                                    │
│  After heapify: [16, 14, 10, 8, 7, 9, 3, 2, 4, 1]        │
│                                                             │
│                         16                                  │
│                      /     \                               │
│                    14       10                             │
│                   /  \     /  \                            │
│                   8    7   9    3                          │
│                  / \  /                                    │
│                 2  4  1                                    │
│                                                             │
│  Step 2: Extract maximum and place at end                  │
│                                                             │
│  Iteration 1: Swap 16 with 1, heapify                     │
│  [14, 8, 10, 4, 7, 9, 3, 2, 1] | [16]                    │
│                                                             │
│  Iteration 2: Swap 14 with 1, heapify                     │
│  [10, 8, 9, 4, 7, 1, 3, 2] | [14, 16]                    │
│                                                             │
│  Iteration 3: Swap 10 with 2, heapify                     │
│  [9, 8, 3, 4, 7, 1, 2] | [10, 14, 16]                    │
│                                                             │
│  Continue until fully sorted...                            │
│                                                             │
│  Final sorted array: [1, 2, 3, 4, 7, 8, 9, 10, 14, 16]   │
└─────────────────────────────────────────────────────────────┘
```

### Build Heap Operation
```
┌─────────────────────────────────────────────────────────────┐
│                   BUILD HEAP OPERATION                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Algorithm: BuildMaxHeap(A[1..n])                          │
│  for i = n/2 down to 1 do                                  │
│      MaxHeapify(A, i)                                      │
│                                                             │
│  Key Insight: Start from last non-leaf node                │
│  • Last non-leaf node is at index n/2                     │
│  • Leaf nodes already satisfy heap property                │
│  • Work bottom-up to ensure heap property                  │
│                                                             │
│  Example with [4, 1, 3, 2, 16, 9, 10, 14, 8, 7]:         │
│                                                             │
│  Initial array as tree:                                    │
│                         4                                   │
│                      /     \                               │
│                     1       3                              │
│                   /  \     /  \                            │
│                   2   16   9   10                          │
│                  / \  /                                    │
│                 14  8 7                                    │
│                                                             │
│  Start from index 5 (last non-leaf):                      │
│  1. Heapify(5): 16 > 9, swap → [4,1,3,2,16,9,10,14,8,7]  │
│  2. Heapify(4): 2 < 14, swap → [4,1,3,14,16,9,10,2,8,7]  │
│  3. Heapify(3): 3 < 10, swap → [4,1,10,14,16,9,10,2,8,7]  │
│  4. Heapify(2): 1 < max(14,16), swap with 16              │
│  5. Heapify(1): 4 < max(16,10), swap with 16              │
│                                                             │
│  Time Complexity: O(n)                                    │
│  • Better than n insertions which would be O(n log n)     │
└─────────────────────────────────────────────────────────────┘
```

## 6. Divide and Conquer Technique

### What is Divide and Conquer?
```
┌─────────────────────────────────────────────────────────────┐
│                 DIVIDE AND CONQUER                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  A problem-solving approach that works by recursively      │
│  breaking down a problem into smaller subproblems          │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    STRATEGY                             │ │
│  │                                                         │ │
│  │  1. DIVIDE: Break problem into smaller subproblems     │ │
│  │  2. CONQUER: Solve subproblems recursively             │ │
│  │  3. COMBINE: Merge solutions to get final answer       │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    STRUCTURE                            │ │
│  │                                                         │ │
│  │                  Original Problem                       │ │
│  │                      /      \                          │ │
│  │               Subproblem1  Subproblem2                  │ │
│  │                  /    \      /    \                    │ │
│  │                Sub1   Sub2  Sub3  Sub4                 │ │
│  │                                                         │ │
│  │  Base Case: Problem small enough to solve directly     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Examples: Binary Search, Merge Sort, Quick Sort           │
└─────────────────────────────────────────────────────────────┘
```

### General Template
```
┌─────────────────────────────────────────────────────────────┐
│              DIVIDE AND CONQUER TEMPLATE                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Algorithm: DivideConquer(problem)                         │
│  {                                                          │
│      if (problem is small enough) {                        │
│          return DirectSolution(problem)  // Base case      │
│      }                                                      │
│      else {                                                 │
│          // Divide                                          │
│          subproblems = Divide(problem)                      │
│                                                             │
│          // Conquer                                         │
│          for each subproblem in subproblems {               │
│              solution[i] = DivideConquer(subproblem[i])     │
│          }                                                  │
│                                                             │
│          // Combine                                         │
│          return Combine(solutions)                          │
│      }                                                      │
│  }                                                          │
│                                                             │
│  Time Complexity: Often T(n) = aT(n/b) + f(n)             │
│  • a = number of subproblems                               │
│  • n/b = size of each subproblem                          │
│  • f(n) = cost of divide and combine                      │
└─────────────────────────────────────────────────────────────┘
```

### 6.1 Binary Search

#### Algorithm and Analysis
```
┌─────────────────────────────────────────────────────────────┐
│                    BINARY SEARCH                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Problem: Find target element in sorted array              │
│                                                             │
│  Algorithm: BinarySearch(A[1..n], target)                  │
│  {                                                          │
│      left = 1, right = n                                   │
│      while (left ≤ right) {                                │
│          mid = (left + right) / 2                          │
│          if (A[mid] == target)                              │
│              return mid                                     │
│          else if (A[mid] < target)                          │
│              left = mid + 1                                │
│          else                                               │
│              right = mid - 1                               │
│      }                                                      │
│      return -1  // Not found                               │
│  }                                                          │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 DIVIDE & CONQUER                        │ │
│  │                                                         │ │
│  │  • DIVIDE: Split array at middle element               │ │
│  │  • CONQUER: Search in appropriate half                 │ │
│  │  • COMBINE: No combining needed                        │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Time Complexity: O(log n)                                │
│  Space Complexity: O(1) iterative, O(log n) recursive     │
│  Recurrence: T(n) = T(n/2) + O(1)                         │
└─────────────────────────────────────────────────────────────┘
```

#### Binary Search Example
```
┌─────────────────────────────────────────────────────────────┐
│                 BINARY SEARCH EXAMPLE                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Array: [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]              │
│  Target: 7                                                 │
│                                                             │
│  Step 1: left=0, right=9, mid=4                           │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 1   3   5   7   9   11  13  15  17  19                 │ │
│  │ ↑               ↑                   ↑                   │ │
│  │left            mid                right                 │ │
│  └─────────────────────────────────────────────────────────┘ │
│  A[4] = 9 > 7, so search left half                        │
│                                                             │
│  Step 2: left=0, right=3, mid=1                           │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 1   3   5   7   |   11  13  15  17  19                 │ │
│  │ ↑   ↑       ↑                                          │ │
│  │left mid    right                                        │ │
│  └─────────────────────────────────────────────────────────┘ │
│  A[1] = 3 < 7, so search right half                       │
│                                                             │
│  Step 3: left=2, right=3, mid=2                           │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │     |   5   7   |                                      │ │
│  │         ↑   ↑                                          │ │
│  │      left/mid right                                     │ │
│  └─────────────────────────────────────────────────────────┘ │
│  A[2] = 5 < 7, so search right half                       │
│                                                             │
│  Step 4: left=3, right=3, mid=3                           │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │             7                                           │ │
│  │             ↑                                           │ │
│  │         left/mid/right                                  │ │
│  └─────────────────────────────────────────────────────────┘ │
│  A[3] = 7 == 7, FOUND! Return index 3                     │
│                                                             │
│  Total comparisons: 4 = ⌈log₂(10)⌉                        │
└─────────────────────────────────────────────────────────────┘
```

### 6.2 Merge Sort

#### Algorithm and Analysis
```
┌─────────────────────────────────────────────────────────────┐
│                      MERGE SORT                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Algorithm: MergeSort(A[1..n])                             │
│  {                                                          │
│      if (n > 1) {                                          │
│          mid = n/2                                         │
│          L = A[1..mid]      // Left half                   │
│          R = A[mid+1..n]    // Right half                  │
│                                                             │
│          MergeSort(L)       // Sort left half              │
│          MergeSort(R)       // Sort right half             │
│                                                             │
│          Merge(A, L, R)     // Merge sorted halves         │
│      }                                                      │
│  }                                                          │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 DIVIDE & CONQUER                        │ │
│  │                                                         │ │
│  │  • DIVIDE: Split array into two halves                 │ │
│  │  • CONQUER: Recursively sort both halves               │ │
│  │  • COMBINE: Merge the sorted halves                    │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Time Complexity: O(n log n) - all cases                  │
│  Space Complexity: O(n)                                   │
│  Recurrence: T(n) = 2T(n/2) + O(n)                        │
│  Stability: Stable sorting algorithm                       │
└─────────────────────────────────────────────────────────────┘
```

#### Merge Sort Example
```
┌─────────────────────────────────────────────────────────────┐
│                   MERGE SORT EXAMPLE                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Input Array: [38, 27, 43, 3, 9, 82, 10]                 │
│                                                             │
│  Divide Phase:                                             │
│                                                             │
│  Level 0:        [38, 27, 43, 3, 9, 82, 10]              │
│                         /            \                     │
│  Level 1:    [38, 27, 43, 3]      [9, 82, 10]            │
│                 /       \           /       \              │
│  Level 2:   [38, 27]   [43, 3]   [9, 82]   [10]          │
│               /  \      /  \      /  \       |             │
│  Level 3:   [38] [27]  [43] [3]  [9] [82]  [10]          │
│                                                             │
│  Conquer Phase (Merge):                                    │
│                                                             │
│  Level 3:   [38] [27]  [43] [3]  [9] [82]  [10]          │
│               \  /      \  /      \  /       |             │
│  Level 2:   [27, 38]   [3, 43]   [9, 82]   [10]          │
│                 \       /           \       /              │
│  Level 1:    [3, 27, 38, 43]      [9, 10, 82]            │
│                         \            /                     │
│  Level 0:        [3, 9, 10, 27, 38, 43, 82]              │
│                                                             │
│  Merge Process Example (Level 2 → Level 1):               │
│  Merge [3, 27, 38, 43] and [9, 10, 82]:                  │
│  • Compare 3 and 9 → take 3                               │
│  • Compare 27 and 9 → take 9                              │
│  • Compare 27 and 10 → take 10                            │
│  • Compare 27 and 82 → take 27                            │
│  • Continue until all elements merged                      │
└─────────────────────────────────────────────────────────────┘
```

### 6.3 Quick Sort

#### Algorithm and Analysis
```
┌─────────────────────────────────────────────────────────────┐
│                      QUICK SORT                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Algorithm: QuickSort(A[low..high])                        │
│  {                                                          │
│      if (low < high) {                                     │
│          pivot = Partition(A, low, high)                   │
│          QuickSort(A, low, pivot-1)                        │
│          QuickSort(A, pivot+1, high)                       │
│      }                                                      │
│  }                                                          │
│                                                             │
│  Partition(A, low, high):                                  │
│  • Choose pivot element (last element)                     │
│  • Rearrange array so elements ≤ pivot are on left        │
│  • Elements > pivot are on right                           │
│  • Return pivot position                                   │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 DIVIDE & CONQUER                        │ │
│  │                                                         │ │
│  │  • DIVIDE: Partition around pivot element              │ │
│  │  • CONQUER: Recursively sort subarrays                 │ │
│  │  • COMBINE: No combining needed (in-place)             │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  Time Complexity:                                          │
│  • Best/Average: O(n log n)                               │
│  • Worst: O(n²) - already sorted array                    │
│  Space Complexity: O(log n) - recursion stack             │
│  Stability: Not stable                                     │
└─────────────────────────────────────────────────────────────┘
```

#### Quick Sort Example
```
┌─────────────────────────────────────────────────────────────┐
│                   QUICK SORT EXAMPLE                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Input Array: [10, 80, 30, 90, 40, 50, 70]               │
│  Pivot Strategy: Last element                              │
│                                                             │
│  Step 1: Initial partition with pivot = 70                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 10  80  30  90  40  50 | 70                            │ │
│  │  ↑                     ↑   ↑                           │ │
│  │  i                     j  pivot                        │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  After partition: [10, 30, 40, 50, 70, 90, 80]           │
│  Elements ≤ 70: [10, 30, 40, 50]                          │
│  Elements > 70: [90, 80]                                   │
│                                                             │
│  Recursively sort left subarray [10, 30, 40, 50]:         │
│  • Pivot = 50                                             │
│  • After partition: [10, 30, 40, 50]                      │
│  • Sort [10, 30, 40] and [] (empty)                       │
│                                                             │
│  Recursively sort right subarray [90, 80]:                │
│  • Pivot = 80                                             │
│  • After partition: [80, 90]                              │
│                                                             │
│  Final sorted array: [10, 30, 40, 50, 70, 80, 90]        │
│                                                             │
│  Partition Process Detail:                                 │
│  i tracks position for next small element                  │
│  j scans through array                                     │
│  Swap when A[j] ≤ pivot                                    │
│  Finally swap pivot to correct position                    │
└─────────────────────────────────────────────────────────────┘
```

### 6.4 Strassen's Matrix Multiplication

#### Standard vs Strassen's Method
```
┌─────────────────────────────────────────────────────────────┐
│               MATRIX MULTIPLICATION                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Problem: Multiply two n×n matrices A and B                │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │             STANDARD METHOD                             │ │
│  │                                                         │ │
│  │  for i = 1 to n do                                     │ │
│  │      for j = 1 to n do                                 │ │
│  │          C[i][j] = 0                                   │ │
│  │          for k = 1 to n do                             │ │
│  │              C[i][j] += A[i][k] * B[k][j]              │ │
│  │                                                         │ │
│  │  Time Complexity: O(n³)                                │ │
│  │  Multiplications: n³                                   │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │            STRASSEN'S METHOD                            │ │
│  │                                                         │ │
│  │  • Divide matrices into 2×2 blocks                     │ │
│  │  • Use 7 multiplications instead of 8                  │ │
│  │  • Recursive approach                                   │ │
│  │                                                         │ │
│  │  Time Complexity: O(n^log₂7) ≈ O(n^2.807)              │ │
│  │  Better for large matrices                              │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

#### Strassen's Algorithm
```
┌─────────────────────────────────────────────────────────────┐
│                STRASSEN'S ALGORITHM                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Divide n×n matrices A, B into 2×2 block matrices:         │
│                                                             │
│  A = [A₁₁  A₁₂]    B = [B₁₁  B₁₂]    C = [C₁₁  C₁₂]       │
│      [A₂₁  A₂₂]        [B₂₁  B₂₂]        [C₂₁  C₂₂]       │
│                                                             │
│  Standard method requires 8 multiplications:               │
│  C₁₁ = A₁₁×B₁₁ + A₁₂×B₂₁                                   │
│  C₁₂ = A₁₁×B₁₂ + A₁₂×B₂₂                                   │
│  C₂₁ = A₂₁×B₁₁ + A₂₂×B₂₁                                   │
│  C₂₂ = A₂₁×B₁₂ + A₂₂×B₂₂                                   │
│                                                             │
│  Strassen's method uses 7 multiplications:                 │
│  M₁ = (A₁₁ + A₂₂) × (B₁₁ + B₂₂)                           │
│  M₂ = (A₂₁ + A₂₂) × B₁₁                                    │
│  M₃ = A₁₁ × (B₁₂ - B₂₂)                                    │
│  M₄ = A₂₂ × (B₂₁ - B₁₁)                                    │
│  M₅ = (A₁₁ + A₁₂) × B₂₂                                    │
│  M₆ = (A₂₁ - A₁₁) × (B₁₁ + B₁₂)                           │
│  M₇ = (A₁₂ - A₂₂) × (B₂₁ + B₂₂)                           │
│                                                             │
│  Then compute:                                             │
│  C₁₁ = M₁ + M₄ - M₅ + M₇                                   │
│  C₁₂ = M₃ + M₅                                             │
│  C₂₁ = M₂ + M₄                                             │
│  C₂₂ = M₁ - M₂ + M₃ + M₆                                   │
│                                                             │
│  Recurrence: T(n) = 7T(n/2) + O(n²)                       │
│  Solution: T(n) = O(n^log₂7) ≈ O(n^2.807)                  │
└─────────────────────────────────────────────────────────────┘
```

### Comparison of Divide and Conquer Algorithms
```
┌─────────────────────────────────────────────────────────────┐
│              ALGORITHM COMPARISON                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┬─────────────┬─────────────┬─────────────┐  │
│  │ Algorithm   │Time Complex │Space Complex│ Stability   │  │
│  ├──────────────┼────────────┼───────────┼─────────────────┤ │
│  │Binary Search│ O(log n)    │ O(1)        │     -         │ │
│  │Merge Sort   │ O(n log n)  │ O(n)        │   Stable      │ │
│  │Quick Sort   │ O(n log n)*  │ O(log n)    │ Not Stable    │ │
│  │Strassen's   │ O(n^2.807)   │ O(n²)       │     -         │ │
│  └──────────────┴────────────┴───────────┴─────────────────┘ │
│  * Average case, O(n²) worst case                          │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   WHEN TO USE                           │ │
│  │                                                         │ │
│  │  Binary Search: Searching in sorted data               │ │
│  │  Merge Sort: When stability is required                │ │
│  │  Quick Sort: General purpose, good average performance │ │
│  │  Strassen's: Very large matrix multiplication          │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
``` 

---

## Quick Revision Points

### Key Algorithm Concepts to Remember:
```
┌─────────────────────────────────────────────────────────────┐
│                    QUICK REFERENCE                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ALGORITHM PROPERTIES:                                      │
│  • Finiteness, Definiteness, Input, Output, Effectiveness  │
│                                                             │
│  ASYMPTOTIC NOTATIONS:                                     │
│  • O(g(n)): Upper bound (≤)                               │
│  • Ω(g(n)): Lower bound (≥)                               │
│  • Θ(g(n)): Tight bound (=)                               │
│                                                             │
│  COMMON COMPLEXITIES (fastest to slowest):                 │
│  • O(1) → O(log n) → O(n) → O(n log n) → O(n²) → O(2ⁿ)   │
│                                                             │
│  DIVIDE & CONQUER STRATEGY:                                │
│  • Divide → Conquer → Combine                             │
│  • Recurrence: T(n) = aT(n/b) + f(n)                      │
└─────────────────────────────────────────────────────────────┘
```

### Important Formulas and Relationships:
```
┌─────────────────────────────────────────────────────────────┐
│                 IMPORTANT FORMULAS                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  HEAP RELATIONSHIPS (0-indexed):                           │
│  • Parent(i) = (i-1)/2                                    │
│  • Left child(i) = 2i + 1                                 │
│  • Right child(i) = 2i + 2                                │
│                                                             │
│  MASTER THEOREM:                                           │
│  T(n) = aT(n/b) + f(n), where a≥1, b>1                    │
│  • If f(n) = O(n^c) where c < log_b(a): T(n) = Θ(n^log_b(a))│
│  • If f(n) = Θ(n^c) where c = log_b(a): T(n) = Θ(n^c log n)│
│  • If f(n) = Ω(n^c) where c > log_b(a): T(n) = Θ(f(n))    │
│                                                             │
│  RECURRENCE SOLUTIONS:                                     │
│  • T(n) = T(n/2) + O(1) → O(log n)      [Binary Search]   │
│  • T(n) = 2T(n/2) + O(n) → O(n log n)   [Merge Sort]      │
│  • T(n) = 7T(n/2) + O(n²) → O(n^2.807)  [Strassen's]     │
└─────────────────────────────────────────────────────────────┘
```

### Algorithm Summary Table:
```
┌─────────────────────────────────────────────────────────────┐
│                 ALGORITHM SUMMARY                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌──────────────┬────────────┬───────────┬─────────────────┐ │
│  │ Algorithm    │ Time       │ Space     │ Key Feature     │ │
│  ├──────────────┼────────────┼───────────┼─────────────────┤ │
│  │ Binary Search│ O(log n)   │ O(1)      │ Sorted array    │ │
│  │ Heap Sort    │ O(n log n) │ O(1)      │ In-place        │ │
│  │ Merge Sort   │ O(n log n) │ O(n)      │ Stable          │ │
│  │ Quick Sort   │ O(n log n)*│ O(log n)  │ Average best    │ │
│  │ Strassen's   │ O(n^2.807) │ O(n²)     │ Large matrices  │ │
│  └──────────────┴────────────┴───────────┴─────────────────┘ │
│  * Average case, O(n²) worst case                          │
│                                                             │
│  HEAP OPERATIONS:                                          │
│  • Insert: O(log n) - Bubble up                           │
│  • Delete: O(log n) - Bubble down                         │
│  • Build Heap: O(n) - Bottom-up approach                  │
│  • Heapify: O(log n) - Maintain heap property             │
└─────────────────────────────────────────────────────────────┘
```

### Exam Tips and Key Points:
```
┌─────────────────────────────────────────────────────────────┐
│                    EXAM TIPS                               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  COMPLEXITY ANALYSIS:                                      │
│  • Drop constants and lower-order terms                    │
│  • Focus on dominant term as n → ∞                        │
│  • Nested loops → multiply complexities                    │
│  • Sequential operations → add complexities                │
│                                                             │
│  DIVIDE & CONQUER IDENTIFICATION:                          │
│  • Problem can be broken into smaller subproblems          │
│  • Subproblems are similar to original problem             │
│  • Solutions can be combined efficiently                   │
│                                                             │
│  HEAP PROPERTIES TO REMEMBER:                              │
│  • Complete binary tree                                    │
│  • Max heap: parent ≥ children                            │
│  • Min heap: parent ≤ children                            │
│  • Height = O(log n)                                      │
│  • Array representation is space-efficient                 │
│                                                             │
│  SORTING ALGORITHM TRADE-OFFS:                             │
│  • Merge Sort: Stable, O(n log n) guaranteed              │
│  • Quick Sort: In-place, good average case                │
│  • Heap Sort: In-place, O(n log n) guaranteed             │
│                                                             │
│  PROBLEM-SOLVING STRATEGY:                                 │
│  1. Understand the problem clearly                         │
│  2. Identify the appropriate technique                     │
│  3. Write the algorithm/pseudocode                         │
│  4. Analyze time and space complexity                      │
│  5. Consider edge cases and optimizations                  │
└─────────────────────────────────────────────────────────────┘
```

### Must Remember for Exams:
1. **Big O Definition**: f(n) = O(g(n)) if ∃ c, n₀ such that f(n) ≤ c×g(n) ∀ n ≥ n₀
2. **Master Theorem**: For solving divide-and-conquer recurrences
3. **Heap Property**: Complete binary tree with parent-child ordering
4. **Divide & Conquer Steps**: Divide → Conquer → Combine
5. **Binary Search Requirement**: Array must be sorted
6. **Merge Sort Stability**: Preserves relative order of equal elements
7. **Quick Sort Pivot**: Choice affects performance significantly
8. **Strassen's Advantage**: Better asymptotic complexity for large matrices

### Common Exam Questions:
- Analyze time complexity of given algorithm
- Trace execution of sorting algorithms
- Design divide-and-conquer solution
- Compare algorithm efficiencies
- Heap operations and properties
- Recurrence relation solving 