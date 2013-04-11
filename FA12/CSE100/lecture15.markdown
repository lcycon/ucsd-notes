# Lecture 15 #

Disjoint Subset ADT
-------------------

- Create(int N)
  - Creates a system of N items, each with it's own equivalence class
- Find (int i)
  - Returns the label of the equivalence class containing item i
- Union (int m, int n)
  - Performs a set union on the equivalence classes with labels m, n, and returns the label

Trees can be used to implement disjoint subsets

- Each tree node represents an item
  - Holds the label, a pointer to to the parent
- Each singleton subset is initally a tree with 1 node
- To find, go to node, return the label of the root
- To union, make the parent of the root of one tree the root of the other

### Smarter Unions ###

- When joining 2 trees, the root of the larger tree should be the root of the new tree
- Could do "union-by-size" or "union-by-height"
- Smart union ensure that height of any tree < log2n
- Union takes O(1), find takes O(log N)

### Path-Compression Find ###

- In normal structure, find requires you to go the node for the item that you want to
  find the equivalence class for, and traverse the parent pointers till you get to the top
- Worst case O(log N)

---

- Path compression find:
  - When you go up, change the parent pointers of each node to point straight to the root!
  - Future finds along that path now cost O(1)

---

- Path-compression is a self-adjusting data structure
- Splay trees, self-adjusting lists, skew heaps are also self-adjusting data structures
- Find operations are more expensive in the hopes that they'll pay off later
- You can use amortized cost analysis to figure out if it pays off

Amortized Cost Analysis
-----------------------

- Considers the time / space cost of doing a sequence of operations
- Using union-by-size or union-by-height and path-compression, any combination of N-1 union
  operations and M find operations has worst-case time cost O(N + M log * N)
- This is almost a constant-time operation when amortized over N-1 + M operations
- log * N
  - The number of times you can take log base 2 of N before you get a number < = 1
  - Practically never greater than 5

Implement parent-pointer trees using arrays
--------------------------------------------

- Create an array A of ints, with length N
- These items have labels 0 - N-1
- If an array element is negative, this element is the root of a tree, where the value is -
  (tree height + 1)
- The element is not a root, the value stored there is the index of the parent
