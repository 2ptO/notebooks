# My personal notes on CS refresher

- [My personal notes on CS refresher](#my-personal-notes-on-cs-refresher)
  - [Core CS](#core-cs)
  - [Language](#language)
  - [Data Structures](#data-structures)
    - [Array/Vectors](#arrayvectors)
    - [String](#string)
    - [Linked lists](#linked-lists)
    - [Trees](#trees)
    - [Stacks and Queues](#stacks-and-queues)
    - [Trie](#trie)
    - [Hash table](#hash-table)
    - [Graphs](#graphs)
    - [Heaps](#heaps)
  - [Algorithms](#algorithms)
    - [Recursion](#recursion)
    - [Sorting](#sorting)
    - [Searching](#searching)
    - [Dynamic Programming](#dynamic-programming)
    - [Math](#math)
  - [System design](#system-design)
  - [Helpful links](#helpful-links)
  - [Python doubts](#python-doubts)

## Core CS

- [ ] Operating systems, principles and concepts ([UCB Lectures](https://archive.org/details/ucberkeley-webcast-PL-XXv-cvA_iBDyz-ba4yDskqMDY6A1w_c) )
- [ ] Computer Networking
- [ ] Storage protocols, applications, pros and cons
- [ ] File system concepts
  - [ ] Distributed File systems
  - [ ] Add relevant links
- [ ] OOP
- [ ] Algorithmic Analysis
  - [ ] Asymptotic Notation
  - [ ] Big O, Omega, Theta notations, derivations
  - [Big O cheat sheet](http://bigocheatsheet.com/)

## Language

- My choice of language: Python. See some refresher vides from this [link](https://github.com/jwasham/coding-interview-university/blob/master/programming-language-resources.md)
- [Python Cheat Sheet](https://github.com/jwasham/coding-interview-university/blob/master/extras/cheat%20sheets/python-cheat-sheet-v1.pdf)
- [ ] Add reference to my own cheat sheet and Python specific notes
- [Complexity in Python](https://www.ics.uci.edu/~pattis/ICS-33/lectures/complexitypython.txt)
- [From python.org](https://wiki.python.org/moin/TimeComplexity)

## Data Structures

### Array/Vectors

- Maximum sub array equaling a given sum (*Kadane's Algorithm*)
- Finding the duplicate number
- Two Sum / Three Sum
- Tools
  - Two pointers - many applications: binary search, two sum problem on sorted nums, finding cycle
  - [1...n], Given an array of length n, with values in range 1..n. Use value as index

### String

- [ ] Suffix arrays
- Substring search algorithms
  - Substrings can be generated two ways..chose the one depending on the problem in hand. Often the second method is preferable, because it solves the smaller substrings first. We can solve subproblems first to apply that to larger problems.
  - For a string of length `n`, there can be `n*(n+1)/2` different substrings
  - Both run in O(n^2)
  ```python
  def gen_substrings(s):
    return {s[i:j+1] for i in range(len(s)) for j in range(i, len(s))}
  
  def gen_substrings2(s):
    return {s[j:i+1] for i in range(len(s) for j in range(i+1))}
  ```
- [ ] Brute force
- [ ] Knuth Morris Pratt
- [ ] Boyer-Moore
- [ ] Rabin Karp

### Linked lists

- [x] All common operations (insertion, deletion, recursion, traversal)
- [x] Finding cycles
  - Use two pointer method. Start both from head. Advance slow pointer by 1 and fast by 2. slow and fast will meet at a point if there exists a cycle.
  ```python
  def has_cycle(head):
    slow = fast = head
    while slow and fast and fast.next:
      slow = slow.next
      fast = fast.next.next
      if fast == slow:
        return True
    return False
  ```
- [x] Finding duplicates/intersection (Floyd's Tortoise/Hare algorithm)
  - Can use simple node wise comparison or hash table based conversion
  - Find the meeting point using cycle detection logic. Then find the intersection using Floyd's algorithm.

### Trees

- Binary Tree / Binary Search Tree
- Traversals
  - [x] BFS - aka level order - using queue
  - [ ] DFS - implement using 1) iterative 2) recursion
  - [x] Pre-order (root-left-right) - applications: tree copy, duplications, prefix notations
    - [x] Iteration: add node to stack, pop from stack, push right followed by left
  - [x] In-order (left-root-right) - applications: binary search trees
    - [x] Normal iteration - go all the way left, at the dead end pop from stack, visit the node and continue on right
    - [ ] Morris inorder iteration
  - [ ] Post-order (left-right-root) - applications: node deletions, polish notations
    - [x] Iteration: left-right-node: go all the way left. peek the stack. if top of the stack has right, visit right first if it is not the last node visited.
- Advanced trees (know the basics at least)
  - [ ] AVL
  - [ ] Splay trees
  - [ ] Red Black
  - [ ] B+ Trees
  - [ ] N-ary tree
- Operations
  - [x] Get height
  - [x] Get min, max
  - [x] Is valid BST?
  - [ ] In-order successor
  - [ ] Delete node

### Stacks and Queues

- [ ] FIFO queue / Circular buffer
- [ ] Priority Queue

### Trie

- [ ] Basics, applications

### Hash table

- Common techniques
  - [ ] Hashing with chaining
  - [ ] Table doubling (Karp Rabin)
  - [ ] Open addressing,
- [ ] Own implementation
- Some links to learn:
  - [How Python Dict works?](https://www.youtube.com/watch?v=C4Kc8xzcA68)
  - [Instant uploads and storage optimization](https://www.coursera.org/learn/data-structures/lecture/DvaIb/instant-uploads-and-storage-optimization-in-dropbox)
  - [Distributed hash tables](https://www.coursera.org/learn/data-structures/lecture/tvH8H/distributed-hash-tables)

### Graphs

- [ ] Add resources
- Basic representation and implementation.
  - [ ] Objects and pointers
  - [ ] Adjacency matrix
  - [ ] Adjacency lists
  - [ ] Adjacency map
- Traversal
  - [ ] BFS, for each representation
  - [ ] DFS, for each representation
  - [ ] Finding cycle
  - [ ] Graph Coloring

### Heaps

- Heaps (Min heap, max heap)
  - Implemented using full binary tree, commonly using arrays/lists
  - operations: push, pop
  - *push* - appends the item to the end, and bubbles it up until heap property is restored
  - *pop* - removes the root (i.e. [0] in the list), replaces it with the last element, bubbles it down until heap property is restored
  - Both *push* and *pop* run in **O(n)** amortized time
- In python, heaps are implemented using *heapq* module
- If two elements compare equal, tiebreaker can be added by inserting elements in tuple form
  ```python
  nums = [random.randint(1, 50) for _ in range(10)]
  heapq.heapify(nums)
  # >>> nums
  # [1, 2, 20, 5, 14, 41, 44, 29, 40, 39]
  heapq.heappush(nums, 34)
  # >>> nums
  # [1, 2, 20, 5, 14, 41, 44, 29, 40, 39, 34]
  n = heapq.heappop(nums)
  # n = 1

  # pushes a value into the heap, bubbles it up and pops the top after insertion
  n = heapq.heappushpop(nums, 4)
  # n = 2
  # >>> nums
  # [4, 5, 20, 29, 14, 41, 44, 34, 40, 39]

  # >>> nums
  # [5, 8, 20, 29, 14, 41, 44, 34, 40, 39]
  # heapreplace pops the top, moves the val into the top and bubble down
  n = heapq.heapreplace(nums, 2)
  # n = 5
  # >>> nums
  # [2, 8, 20, 29, 14, 41, 44, 34, 40, 39]
  ```
- HeapSort - throw the values to be sorted into heap, pop one at a time.
  ```python
  nums = [2, 8, 20, 8, 14, 39, 41, 29, 40, 39]
  sorted_nums = [heapq.heappop(nums) for _ in range(len(nums))]
  ```
- Priority Queue
  Much like the heapq operations, but this is often used in multi threaded environment to provide a producer/consumer style message processing. Provides synchronization through locking
  ```python
  from queue import PriorityQueue

  pq = PriorityQueue()

  for num in [2, 8, 20, 8, 14, 39, 41, 29, 40, 39]:
    pq.put(num)
  
  sorted_nums = []
  while not pq.empty():
    sorted_nums.append(pq.get())
  ```

## Algorithms

### Recursion

- [Tail recursion](https://www.quora.com/What-is-tail-recursion-Why-is-it-so-bad)

### Sorting

- Merge sort
- Quick sort
- Bubble sort
- Insertion sort
- Selection sort
- Radix sort
- Stability
- Choice of data structure (linked lists vs arrays)
- Complexities of different sorting algorithms
- [Some advanced concepts](https://www.youtube.com/watch?v=cNB2lADK3_s)

### Searching

- [ ] Binary search
- [ ] Sliding window
- [ ] Two pointers
- [ ] DFS
- [ ] BFS
  
### Dynamic Programming

- [ ] NP, NP-Complete and Approximation algorithms
- [ ] Backtracking
- [ ] Greedy

### Math

- [ ] Probability
- [ ] Combinations
- [ ] Permutations

## System design

To be added

## Helpful links

- [Interactive Challenges](https://github.com/donnemartin/interactive-coding-challenges)

## Python doubts

- Is there === in python? No. '==' is rightly overloaded to cover the equality checks. See this [link](https://stackoverflow.com/questions/44425359/is-there-any-python-operator-that-equivalent-to-javascript-triple-equal)
