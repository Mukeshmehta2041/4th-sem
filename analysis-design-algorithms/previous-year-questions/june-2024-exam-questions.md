# June 2024 Exam Questions - Analysis Design of Algorithm

**Course:** CS/SD-402 (GS) B.Tech., IV Semester  
**Examination:** June 2024  
**Time:** Three Hours  
**Maximum Marks:** 70  
**Total Questions:** 8 (Attempt any five)

---

## Question 1

**a)** Obtain the asymptotic bound using the substitution method for the recurrence relation T(n) = 3T(n/3) + n and represent it in terms of θ notation.

**b)** What is Merge sort? Sort the elements 20, 30, 15, 11, 35, 19, 12, 11, 55 using Merge sort.

---

## Question 2

**a)** Discuss Strassen's matrix multiplication and Classical O(n²) methods. Determine when Strassen's method outperforms classical method.

**b)** Define spanning tree? Construct a minimal spanning tree for the given graph using Prim's algorithm.

*Graph Details:*
- 6 nodes labeled 1 through 6
- Edges with weights:
  - (1,2): weight 6, (1,3): weight 5, (1,4): weight 5
  - (2,3): weight 5, (2,5): weight 3
  - (3,4): weight 5, (3,6): weight 6
  - (4,6): weight 2
  - (5,6): weight 6

---

## Question 3

Solve the following problem of job sequencing with deadlines using the Greedy method.

**Given:** n = 4, (p₁, p₂, p₃, p₄) = (100, 10, 15, 27) and (d₁, d₂, d₃, d₄) = (2, 1, 2, 1).

---

## Question 4

**a)** Apply the greedy method to solve the 0/1 Knapsack problem for n = 3, m = 20, (w₁, w₂, w₃) = (18, 15, 10) and (p₁, p₂, p₃) = (25, 24, 15).

**b)** Construct a multistage graph for the given graph using the greedy method.

*Multistage Graph Details:*
- 12 nodes labeled 1 through 12, plus node 't' next to node 12
- Nodes arranged in 5 stages:
  - Stage 1: Node 1
  - Stage 2: Nodes 2, 3, 4, 5
  - Stage 3: Nodes 6, 7, 8
  - Stage 4: Nodes 9, 10, 11
  - Stage 5: Node 12
- Various weighted edges between stages

---

## Question 5

**a)** Explain the Floyd Warshall algorithm for the given graph.

*Directed Graph Details:*
- 4 nodes labeled 1, 2, 3, 4
- Edges: 1→2 (weight -2), 2→3 (weight 3), 3→4 (weight 2), 4→2 (weight -1)

**b)** Using branch and bound technique explain the 0/1 knapsack problem.

---

## Question 6

**a)** Give the solution to the 8-queens problem using backtracking.

**b)** What is graph coloring? Explain graph coloring for the given graph.

*Undirected Graph Details:*
- 6 nodes labeled a, b, c, d, e, f
- Nodes 'a', 'b', 'e', 'f' form rectangle corners
- Nodes 'c' and 'd' inside rectangle
- Edges: (a,b), (b,f), (f,e), (e,a), (a,c), (b,c), (c,d), (d,e), (d,f)

---

## Question 7

**a)** Use the function OBST to compute w(i,j), r(i,j) and c(i,j), 0 ≤ i < j ≤ 4 for the identifier set (a₁, a₂, a₃, a₄) = (char, float, while, else) with p(1) = 1/20, p(2) = 1/5, p(3) = 1/10, p(4) = 1/20, q(0) = 1/5, q(1) = 1/10, q(2) = 1/5, q(3) = 1/5, q(4) = 1/20. Using r(i,j)'s construct the optimal binary search tree.

**b)** Explain in detail about 2-3 Trees with an example.

---

## Question 8

Write short notes on any two of the following:

**a)** Binary search algorithm and its time complexity

**b)** Single source shortest path algorithm

**c)** Parallel algorithms

**d)** NP Completeness

---

*Source: CS/SD-402 (GS) B.Tech., IV Semester Examination, June 2024* 