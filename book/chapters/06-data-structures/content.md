# Chapter 6: Data Structures & Algorithms

---

## Chapter Overview

- **Domain**: Computer Science Fundamentals
- **Estimated Study Time**: 6-7 hours
- **Prerequisites**: Basic programming concepts, logical thinking
- **Difficulty Progression**: Beginner → Intermediate → Advanced → Expert

---

## Learning Objectives

By the end of this chapter, you will be able to:

1. **Define** fundamental data structures and **explain** their characteristics and use cases (B)
2. **Describe** array, linked list, stack, and queue operations and implementations (B)
3. **Implement** tree traversal algorithms and hash table operations (I)
4. **Apply** appropriate sorting and searching algorithms for different scenarios (I)
5. **Analyze** algorithm complexity using Big O notation and **compare** algorithm efficiency (A)
6. **Evaluate** graph algorithms including shortest path and minimum spanning tree (A)
7. **Design** solutions using dynamic programming and divide-and-conquer approaches (E)
8. **Assess** algorithm selection based on problem constraints and performance requirements (E)

---

## Introduction

Data structures and algorithms form the theoretical foundation of computer science and software development. Understanding how data is organized, stored, and manipulated is essential for evaluating software solutions, understanding system performance, and making informed technology decisions.

As an Assistant Director IT, you may not write code daily, but understanding these concepts enables you to evaluate vendor proposals, assess technical feasibility, communicate effectively with development teams, and understand why certain solutions perform better than others.

This chapter covers fundamental data structures, common algorithms, and complexity analysis. These concepts connect to database management (Chapter 5), programming (Chapter 25), and system design principles used throughout IT infrastructure.

---

## Section 6.1: Linear Data Structures (B)

Linear data structures organize elements in a sequential manner, where each element has a predecessor and successor (except for the first and last elements).

### 6.1.1 Arrays

An array is a collection of elements stored in contiguous memory locations, accessed by index.

**Characteristics**:
- Fixed size (in most languages)
- O(1) access by index
- O(n) insertion/deletion (requires shifting)
- Efficient memory usage

**Array Types**:

| Type | Description | Access Pattern |
|------|-------------|----------------|
| One-dimensional | Linear sequence | arr[i] |
| Two-dimensional | Matrix/grid | arr[i][j] |
| Multi-dimensional | Higher dimensions | arr[i][j][k]... |

**Common Operations**:
| Operation | Time Complexity |
|-----------|-----------------|
| Access by index | O(1) |
| Search (unsorted) | O(n) |
| Search (sorted) | O(log n) |
| Insert at end | O(1) amortized |
| Insert at position | O(n) |
| Delete at position | O(n) |

### 6.1.2 Linked Lists

A linked list is a sequence of nodes where each node contains data and a reference to the next node.

**Types of Linked Lists**:

**Singly Linked List**:
```
[Data|Next] → [Data|Next] → [Data|Next] → NULL
    Head                                    Tail
```

**Doubly Linked List**:
```
NULL ← [Prev|Data|Next] ↔ [Prev|Data|Next] ↔ [Prev|Data|Next] → NULL
              Head                                    Tail
```

**Circular Linked List**:
```
[Data|Next] → [Data|Next] → [Data|Next] → (back to Head)
    Head
```

**Linked List vs Array**:

| Aspect | Array | Linked List |
|--------|-------|-------------|
| Memory allocation | Contiguous | Non-contiguous |
| Access | O(1) by index | O(n) by traversal |
| Insertion/Deletion | O(n) | O(1) at known position |
| Memory overhead | Low | Higher (pointers) |
| Cache performance | Better | Worse |

### Practical Example 6.1: When to Use Linked Lists

**Scenario**: A government agency needs to maintain a queue of citizen service requests.

**Analysis**:
- Frequent additions at the end
- Frequent removals from the front
- Size varies unpredictably
- No need for random access

**Recommendation**: Linked list (or deque) is appropriate due to frequent insertions/deletions at both ends with O(1) complexity.

### 6.1.3 Stacks

A stack is a Last-In-First-Out (LIFO) data structure. Elements are added and removed from the same end (top).

**Operations**:
| Operation | Description | Complexity |
|-----------|-------------|------------|
| push(item) | Add item to top | O(1) |
| pop() | Remove and return top item | O(1) |
| peek()/top() | View top item without removing | O(1) |
| isEmpty() | Check if stack is empty | O(1) |

**Applications**:
- Function call stack (recursion)
- Expression evaluation and parsing
- Undo/redo functionality
- Backtracking algorithms
- Syntax validation (balanced parentheses)

### Practical Example 6.2: Balanced Parentheses

**Problem**: Check if parentheses in an expression are balanced.

**Algorithm using Stack**:
```
Input: "((a+b)*(c-d))"

Process:
1. '(' → push → Stack: ['(']
2. '(' → push → Stack: ['(', '(']
3. 'a', '+', 'b' → ignore
4. ')' → pop → Stack: ['(']
5. '*' → ignore
6. '(' → push → Stack: ['(', '(']
7. 'c', '-', 'd' → ignore
8. ')' → pop → Stack: ['(']
9. ')' → pop → Stack: []

Final: Stack is empty → Balanced ✓
```

### 6.1.4 Queues

A queue is a First-In-First-Out (FIFO) data structure. Elements are added at the rear and removed from the front.

**Operations**:
| Operation | Description | Complexity |
|-----------|-------------|------------|
| enqueue(item) | Add item to rear | O(1) |
| dequeue() | Remove and return front item | O(1) |
| front()/peek() | View front item | O(1) |
| isEmpty() | Check if queue is empty | O(1) |

**Queue Variants**:

**Circular Queue**:
- Fixed-size array with wraparound
- Efficient use of space
- Used in buffer management

**Priority Queue**:
- Elements have priorities
- Highest priority dequeued first
- Implemented using heaps
- Used in scheduling, Dijkstra's algorithm

**Deque (Double-Ended Queue)**:
- Insertion/deletion at both ends
- Combines stack and queue properties

**Applications**:
- Process scheduling (OS)
- Print job queue
- Breadth-first search
- Message queues
- Request handling in web servers

---

## Section 6.2: Non-Linear Data Structures (I)

Non-linear data structures organize elements in hierarchical or interconnected relationships.

### 6.2.1 Trees

A tree is a hierarchical data structure with a root node and subtrees of children.

**Tree Terminology**:
| Term | Definition |
|------|------------|
| Root | Top node (no parent) |
| Node | Element in the tree |
| Edge | Connection between nodes |
| Parent | Node directly above |
| Child | Node directly below |
| Leaf | Node with no children |
| Height | Longest path from root to leaf |
| Depth | Distance from root to node |
| Subtree | Tree formed by a node and its descendants |

**Binary Tree**: Each node has at most two children (left and right).

**Binary Search Tree (BST)**: A binary tree where:
- Left subtree contains only nodes with values less than the node
- Right subtree contains only nodes with values greater than the node
- Both subtrees are also BSTs

```
        8
       / \
      3   10
     / \    \
    1   6    14
       / \   /
      4   7 13
```

**BST Operations**:
| Operation | Average | Worst (unbalanced) |
|-----------|---------|-------------------|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |

### 6.2.2 Tree Traversals

**Depth-First Traversals**:

**Inorder (Left, Root, Right)** - BST gives sorted order:
```
Result: 1, 3, 4, 6, 7, 8, 10, 13, 14
```

**Preorder (Root, Left, Right)** - Used to copy a tree:
```
Result: 8, 3, 1, 6, 4, 7, 10, 14, 13
```

**Postorder (Left, Right, Root)** - Used to delete a tree:
```
Result: 1, 4, 7, 6, 3, 13, 14, 10, 8
```

**Breadth-First Traversal (Level Order)**:
```
Result: 8, 3, 10, 1, 6, 14, 4, 7, 13
```

### 6.2.3 Balanced Trees

Balanced trees maintain O(log n) height to ensure efficient operations.

**AVL Tree**:
- Self-balancing BST
- Balance factor (height difference) ≤ 1 for all nodes
- Rotations used to maintain balance

**Red-Black Tree**:
- Self-balancing BST with color properties
- No two consecutive red nodes
- Same number of black nodes on all paths to leaves
- Used in many standard library implementations

**B-Tree and B+ Tree**:
- Generalized BST for disk-based storage
- Multiple keys per node
- Used in database indexes
- B+ Tree: All data in leaf nodes, linked for range queries

### Practical Example 6.3: Tree Applications

**Scenario**: Database index design for employee search.

**B+ Tree Index**:
- Each node holds multiple keys (e.g., employee IDs)
- Leaf nodes contain all data and are linked
- Efficient for both point queries and range queries
- Minimizes disk I/O

**Benefits**:
- Search: O(log n) with low constant factor
- Range queries: Efficient due to linked leaves
- Balanced: Guaranteed performance

### 6.2.4 Heaps

A heap is a complete binary tree satisfying the heap property.

**Max-Heap**: Parent ≥ children
**Min-Heap**: Parent ≤ children

```
Max-Heap:
        90
       /  \
      79   72
     / \   / \
    55 60 48 35
```

**Heap Operations**:
| Operation | Complexity |
|-----------|------------|
| Insert | O(log n) |
| Extract max/min | O(log n) |
| Get max/min | O(1) |
| Heapify | O(n) |

**Applications**:
- Priority queues
- Heap sort
- Finding k largest/smallest elements
- Dijkstra's and Prim's algorithms

### 6.2.5 Graphs

A graph consists of vertices (nodes) and edges (connections).

**Graph Types**:
| Type | Description |
|------|-------------|
| Directed | Edges have direction |
| Undirected | Edges are bidirectional |
| Weighted | Edges have values/costs |
| Unweighted | All edges equal |
| Connected | Path exists between all vertices |
| Cyclic | Contains at least one cycle |
| Acyclic | No cycles (e.g., DAG) |

**Graph Representations**:

**Adjacency Matrix**:
```
    A B C D
A [ 0 1 1 0 ]
B [ 1 0 1 1 ]
C [ 1 1 0 1 ]
D [ 0 1 1 0 ]
```
- O(V²) space
- O(1) edge lookup
- Good for dense graphs

**Adjacency List**:
```
A → [B, C]
B → [A, C, D]
C → [A, B, D]
D → [B, C]
```
- O(V + E) space
- O(degree) edge lookup
- Good for sparse graphs

### 6.2.6 Graph Traversals

**Breadth-First Search (BFS)**:
- Visits neighbors before going deeper
- Uses a queue
- Finds shortest path in unweighted graphs
- Level-order exploration

**Depth-First Search (DFS)**:
- Explores as far as possible before backtracking
- Uses a stack (or recursion)
- Used in topological sorting, cycle detection
- Explores depth-first

### Practical Example 6.4: Network Topology Analysis

**Scenario**: Analyze network connectivity using BFS.

**Problem**: Find all devices reachable from the main router within 2 hops.

**BFS Algorithm**:
```
Start: Router
Level 0: [Router]
Level 1: [Switch1, Switch2, Firewall]
Level 2: [Server1, Server2, PC1-10, ...Printer]

Result: All devices at level 0-2 are reachable within 2 hops
```

---

## Section 6.3: Hash-Based Structures (I)

Hash tables provide efficient key-value storage with average O(1) operations.

### 6.3.1 Hash Tables

A hash table uses a hash function to map keys to array indices.

**Components**:
- **Hash function**: Converts key to index
- **Array (buckets)**: Stores values
- **Collision handling**: Manages key collisions

**Hash Function Properties**:
- Deterministic (same input = same output)
- Uniform distribution
- Fast computation
- Minimize collisions

### 6.3.2 Collision Resolution

**Chaining (Separate Chaining)**:
- Each bucket contains a linked list
- Multiple keys can exist at same index
- Performance degrades with long chains

```
Index 0: [key1:val1] → [key5:val5]
Index 1: [key2:val2]
Index 2: [key3:val3] → [key6:val6] → [key9:val9]
Index 3: NULL
Index 4: [key4:val4]
```

**Open Addressing**:
- Find alternative empty slot
- Types:
  - **Linear Probing**: Check next slot sequentially
  - **Quadratic Probing**: Check slots at increasing squared distances
  - **Double Hashing**: Use second hash function for step size

**Hash Table Operations**:
| Operation | Average | Worst |
|-----------|---------|-------|
| Insert | O(1) | O(n) |
| Search | O(1) | O(n) |
| Delete | O(1) | O(n) |

**Load Factor**: α = n/m (elements/buckets)
- When α exceeds threshold, resize and rehash
- Typical threshold: 0.7-0.8

### Practical Example 6.5: Hash Table for Caching

**Scenario**: Implement a cache for frequently accessed citizen records.

**Design**:
```
Key: Citizen ID (CNIC)
Value: Citizen Record Object
Hash Function: Hash(CNIC) mod table_size

Benefits:
- O(1) average lookup
- Efficient memory usage
- Fast cache hits/misses
```

---

## Section 6.4: Sorting Algorithms (I)

Sorting algorithms arrange elements in a specific order.

### 6.4.1 Comparison-Based Sorts

**Bubble Sort**:
- Compare adjacent elements, swap if out of order
- Repeat until sorted
- Simple but inefficient

| Best | Average | Worst | Space | Stable |
|------|---------|-------|-------|--------|
| O(n) | O(n²) | O(n²) | O(1) | Yes |

**Selection Sort**:
- Find minimum, swap to front
- Repeat for remaining elements

| Best | Average | Worst | Space | Stable |
|------|---------|-------|-------|--------|
| O(n²) | O(n²) | O(n²) | O(1) | No |

**Insertion Sort**:
- Build sorted portion by inserting each element
- Efficient for small or nearly sorted data

| Best | Average | Worst | Space | Stable |
|------|---------|-------|-------|--------|
| O(n) | O(n²) | O(n²) | O(1) | Yes |

**Merge Sort**:
- Divide array into halves
- Recursively sort each half
- Merge sorted halves
- Guaranteed O(n log n)

| Best | Average | Worst | Space | Stable |
|------|---------|-------|-------|--------|
| O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |

**Quick Sort**:
- Choose pivot element
- Partition: smaller elements left, larger right
- Recursively sort partitions
- Often fastest in practice

| Best | Average | Worst | Space | Stable |
|------|---------|-------|-------|--------|
| O(n log n) | O(n log n) | O(n²) | O(log n) | No |

**Heap Sort**:
- Build max-heap from array
- Repeatedly extract maximum
- In-place, guaranteed O(n log n)

| Best | Average | Worst | Space | Stable |
|------|---------|-------|-------|--------|
| O(n log n) | O(n log n) | O(n log n) | O(1) | No |

### 6.4.2 Non-Comparison Sorts

**Counting Sort**:
- Count occurrences of each value
- Works for integers in known range
- O(n + k) where k is range

**Radix Sort**:
- Sort by individual digits
- Uses counting sort as subroutine
- O(d × (n + k)) where d is number of digits

**Bucket Sort**:
- Distribute elements into buckets
- Sort each bucket
- Concatenate results
- O(n) average with uniform distribution

### Practical Example 6.6: Algorithm Selection

**Scenario**: Sort citizen records by ID for different use cases.

| Use Case | Recommended | Reason |
|----------|-------------|--------|
| Large dataset, unknown distribution | Quick Sort (with random pivot) | Fast average case |
| Stability required | Merge Sort | Preserves equal element order |
| Limited memory | Heap Sort | In-place, O(1) extra space |
| Small dataset (<50 elements) | Insertion Sort | Low overhead |
| Integer keys in known range | Counting/Radix Sort | O(n) possible |

---

## Section 6.5: Searching Algorithms (I)

Searching algorithms locate elements in data structures.

### 6.5.1 Linear Search

- Examine each element sequentially
- Works on unsorted data
- O(n) time complexity

### 6.5.2 Binary Search

- Requires sorted data
- Divide search space in half each step
- O(log n) time complexity

**Algorithm**:
```
function binarySearch(arr, target):
    left = 0
    right = length(arr) - 1

    while left <= right:
        mid = (left + right) / 2

        if arr[mid] == target:
            return mid
        else if arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1  // Not found
```

**Binary Search Variants**:
- Find first/last occurrence
- Find insertion point
- Find floor/ceiling value

### 6.5.3 Interpolation Search

- Estimates position based on value distribution
- O(log log n) for uniformly distributed data
- O(n) worst case

---

## Section 6.6: Graph Algorithms (A)

Advanced graph algorithms solve complex connectivity and optimization problems.

### 6.6.1 Shortest Path Algorithms

**Dijkstra's Algorithm**:
- Finds shortest path from source to all vertices
- Works with non-negative edge weights
- Uses priority queue (min-heap)
- O((V + E) log V) with binary heap

**Algorithm Steps**:
1. Initialize distances: source = 0, all others = ∞
2. Add source to priority queue
3. While queue not empty:
   - Extract vertex with minimum distance
   - For each neighbor:
     - If new distance shorter, update and add to queue
4. Return distance array

### Practical Example 6.7: Network Routing

**Scenario**: Find shortest path between two offices in a WAN.

**Network Graph**:
```
       10
   A ──────── B
   │         │
 5 │         │ 3
   │    2    │
   C ──────── D
         │
       7 │
         E
```

**Dijkstra from A**:
| Step | Current | Distances |
|------|---------|-----------|
| Init | - | A=0, B=∞, C=∞, D=∞, E=∞ |
| 1 | A | A=0, B=10, C=5, D=∞, E=∞ |
| 2 | C | A=0, B=10, C=5, D=7, E=12 |
| 3 | D | A=0, B=10, C=5, D=7, E=12 |
| 4 | B | A=0, B=10, C=5, D=7, E=12 |
| 5 | E | A=0, B=10, C=5, D=7, E=12 |

**Result**: Shortest path A→E = 12 (A→C→D→E)

**Bellman-Ford Algorithm**:
- Handles negative edge weights
- Detects negative cycles
- O(V × E) time complexity

### 6.6.2 Minimum Spanning Tree

A minimum spanning tree (MST) connects all vertices with minimum total edge weight.

**Prim's Algorithm**:
- Grows MST from starting vertex
- Always add minimum weight edge to tree
- Uses priority queue
- O((V + E) log V)

**Kruskal's Algorithm**:
- Sort all edges by weight
- Add edges that don't create cycles
- Uses Union-Find data structure
- O(E log E)

### Practical Example 6.8: Network Infrastructure

**Scenario**: Connect 5 office buildings with minimum cabling cost.

**Graph**:
```
A-B: 4, A-C: 2, B-C: 1, B-D: 5, C-D: 8, C-E: 3, D-E: 6
```

**Kruskal's Algorithm**:
1. Sort edges: (B-C,1), (A-C,2), (C-E,3), (A-B,4), (B-D,5), (D-E,6), (C-D,8)
2. Add B-C (1) ✓
3. Add A-C (2) ✓
4. Add C-E (3) ✓
5. Skip A-B (creates cycle A-B-C)
6. Add B-D (5) ✓
7. MST complete: {B-C, A-C, C-E, B-D}, Total: 11

---

## Section 6.7: Complexity Analysis (A)

Complexity analysis measures algorithm efficiency in terms of time and space.

### 6.7.1 Big O Notation

Big O describes the upper bound (worst case) of an algorithm's growth rate.

**Common Complexities** (sorted by efficiency):

| Notation | Name | Example |
|----------|------|---------|
| O(1) | Constant | Array access |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Linear search |
| O(n log n) | Linearithmic | Merge sort |
| O(n²) | Quadratic | Bubble sort |
| O(n³) | Cubic | Matrix multiplication |
| O(2ⁿ) | Exponential | Recursive Fibonacci |
| O(n!) | Factorial | Permutations |

### 6.7.2 Other Notations

**Big Omega (Ω)**: Lower bound (best case)
**Big Theta (Θ)**: Tight bound (average case)

### 6.7.3 Space Complexity

Space complexity measures memory usage:
- **Auxiliary space**: Extra space beyond input
- **Total space**: Input + auxiliary

**Examples**:
| Algorithm | Time | Space |
|-----------|------|-------|
| Merge Sort | O(n log n) | O(n) |
| Quick Sort | O(n log n) avg | O(log n) |
| Heap Sort | O(n log n) | O(1) |

### Practical Example 6.9: Complexity Comparison

**Scenario**: Process 1 million records. Compare algorithm times.

| Complexity | Operations | Time (1μs/op) |
|------------|------------|---------------|
| O(log n) | ~20 | 20 μs |
| O(n) | 1,000,000 | 1 second |
| O(n log n) | ~20,000,000 | 20 seconds |
| O(n²) | 10¹² | ~12 days |
| O(2ⁿ) | Astronomically large | Heat death of universe |

**Insight**: Algorithm choice critically impacts feasibility for large datasets.

---

## Section 6.8: Algorithm Design Paradigms (E)

### 6.8.1 Divide and Conquer

Split problem into subproblems, solve recursively, combine solutions.

**Steps**:
1. **Divide**: Break problem into smaller subproblems
2. **Conquer**: Solve subproblems recursively
3. **Combine**: Merge subproblem solutions

**Examples**: Merge Sort, Quick Sort, Binary Search, Strassen's Matrix Multiplication

### 6.8.2 Dynamic Programming

Solve complex problems by breaking into overlapping subproblems.

**Characteristics**:
- Optimal substructure: Optimal solution contains optimal solutions to subproblems
- Overlapping subproblems: Same subproblems solved multiple times

**Approaches**:
- **Top-down (Memoization)**: Recursive with caching
- **Bottom-up (Tabulation)**: Iterative, build up solution

**Classic Problems**:
- Fibonacci sequence
- Longest Common Subsequence
- Knapsack problem
- Shortest path (Floyd-Warshall)

### Practical Example 6.10: Fibonacci Comparison

**Naive Recursive** (O(2ⁿ)):
```
fib(n) = fib(n-1) + fib(n-2)
fib(40) takes ~1 minute
```

**Dynamic Programming** (O(n)):
```
dp[0] = 0, dp[1] = 1
for i = 2 to n:
    dp[i] = dp[i-1] + dp[i-2]
fib(40) takes <1 ms
```

### 6.8.3 Greedy Algorithms

Make locally optimal choice at each step, hoping for global optimum.

**Characteristics**:
- Make best choice at each step
- Don't reconsider past choices
- Efficient but may not find optimal solution

**When Greedy Works**:
- Activity selection
- Huffman coding
- Dijkstra's algorithm
- Prim's/Kruskal's MST

### 6.8.4 Backtracking

Systematically explore all possibilities, abandoning paths that can't lead to solutions.

**Applications**:
- N-Queens problem
- Sudoku solver
- Graph coloring
- Maze solving

---

## Hands-on Labs

### Lab 6.1: Array and Linked List Operations

See [labs/lab-06-01-linear-structures.md](labs/lab-06-01-linear-structures.md) for complete lab instructions.

**Objective**: Implement and compare array and linked list operations.

### Lab 6.2: Tree Traversals and BST Operations

See [labs/lab-06-02-trees.md](labs/lab-06-02-trees.md) for complete lab instructions.

**Objective**: Implement tree traversals and BST search, insert, delete.

### Lab 6.3: Sorting Algorithm Comparison

See [labs/lab-06-03-sorting.md](labs/lab-06-03-sorting.md) for complete lab instructions.

**Objective**: Implement and benchmark multiple sorting algorithms.

### Lab 6.4: Graph Algorithms

See [labs/lab-06-04-graphs.md](labs/lab-06-04-graphs.md) for complete lab instructions.

**Objective**: Implement BFS, DFS, and Dijkstra's algorithm.

### Lab 6.5: Hash Table Implementation

See [labs/lab-06-05-hashtables.md](labs/lab-06-05-hashtables.md) for complete lab instructions.

**Objective**: Build a hash table with collision handling.

---

## Chapter Summary

Key points covered in this chapter:

- Linear data structures (arrays, linked lists, stacks, queues) organize data sequentially with different trade-offs for access and modification.
- Trees provide hierarchical organization; binary search trees enable O(log n) operations when balanced.
- Tree traversals (inorder, preorder, postorder, level-order) visit nodes in different orders for different purposes.
- Heaps implement efficient priority queues with O(log n) insertion and extraction.
- Graphs model relationships; represented by adjacency matrices (dense) or lists (sparse).
- Hash tables provide O(1) average-case operations using hash functions and collision resolution.
- Sorting algorithms range from O(n²) (bubble, selection) to O(n log n) (merge, quick, heap) to O(n) (counting, radix for integers).
- Binary search achieves O(log n) searching in sorted data.
- Graph algorithms solve shortest path (Dijkstra, Bellman-Ford) and minimum spanning tree (Prim, Kruskal) problems.
- Big O notation describes algorithm complexity; choosing appropriate algorithms is critical for large datasets.

---

## Key Takeaways

1. **Data structure selection impacts performance**: Choosing between arrays, linked lists, trees, and hash tables depends on access patterns and operations needed.

2. **Balanced trees are essential**: Unbalanced BSTs degrade to O(n); AVL and Red-Black trees maintain O(log n) operations.

3. **Hash tables provide the fastest average-case lookup**: But require good hash functions and collision handling.

4. **Know your sorting algorithms**: Quick sort is often fastest in practice; merge sort guarantees O(n log n); use counting/radix for integers.

5. **Algorithm complexity determines feasibility**: An O(n²) algorithm may be unusable for large n; always analyze complexity for production systems.

---

## Self-Assessment Questions

Answer these questions in your own words (2-3 paragraphs each):

1. **Compare arrays and linked lists** for implementing a queue that handles thousands of service requests per second. Which would you recommend and why? (B/I)

2. **Explain the difference between BFS and DFS graph traversals**. When would you use each, and what are their time/space complexities? (I/A)

3. **Given a hash table with 1000 buckets and 800 elements**, calculate the load factor. What happens if we insert 500 more elements? Explain collision resolution strategies. (A)

4. **Compare merge sort and quick sort** for sorting 10 million employee records. Consider time complexity, space requirements, and stability. Which would you recommend? (A)

5. **Design an algorithm** to find the shortest path for emergency vehicles across a city road network with varying traffic conditions. What algorithm would you use and why? What if some roads had construction (negative impact on travel time)? (E)

---

## Chapter MCQs

See [mcqs.md](mcqs.md) for complete MCQ set with:
- 45 Beginner (B) questions (25%)
- 63 Intermediate (I) questions (35%)
- 54 Advanced (A) questions (30%)
- 18 Expert (E) questions (10%)

Total: 180 MCQs

---

## References

- Cormen, Thomas H., et al. "Introduction to Algorithms." 4th Edition. MIT Press, 2022.
- Sedgewick, Robert, and Kevin Wayne. "Algorithms." 4th Edition. Addison-Wesley, 2011.
- Skiena, Steven S. "The Algorithm Design Manual." 3rd Edition. Springer, 2020.
- Goodrich, Michael T., and Roberto Tamassia. "Data Structures and Algorithms in Python." Wiley, 2013.
- Knuth, Donald E. "The Art of Computer Programming." Volumes 1-4A. Addison-Wesley.
- GeeksforGeeks. "Data Structures and Algorithms." https://www.geeksforgeeks.org/
- MIT OpenCourseWare. "6.006 Introduction to Algorithms." https://ocw.mit.edu/

---

**Chapter Status**: Draft
**Last Updated**: 2026-02-01
**Author**: Content Development Team
**Reviewer**: Pending Technical Review
