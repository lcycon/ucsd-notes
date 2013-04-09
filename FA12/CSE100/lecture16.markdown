# Lecture 16 #

Memory Access
-------------

- In simple algorithmic analysis, memory access is assumed to be O(1)

		Ammount of storage | Location  | Access Time
		-------------------|-----------|----------------
		Hundreds of bytes  | Registers | 1 nanosecond
		-------------------|-----------|----------------
		Hundreds of kbytes | Cache     | 10 nanoseconds
		-------------------|-----------|----------------
		Hundreds of mbytes | Memory    | 100 nanoseconds
		-------------------|-----------|----------------
		Hundreds of gbytes | Disk      | 10 milliseconds

- Accessing a variable could be fast or slow, depending on various factors
- When a variable is accessed, it is often cached

Accessing data on disk
----------------------

- Data is organized into blocks, each block is between 1kb and 4kb
- Entire blocks are read at a time
- For this reason, large DBs use B-trees

B-trees
-------

- B-trees are search trees
- They are NOT binary trees
- B-trees are balanced
  - All of their leaves are at the same level
- A node in a B-tree is designed to fit into one disk block
  - When a node is accessed, it's entire contents are read into main memory
  - Large branching factor: tree is not very deep

### B Tree Properties ###

- Depends of factors M, L, which are selected to maximize performance
- In a B+ tree, data records are stored only in the leaves
  - Leaves always hold between ceil(L/2) and L data records inclusive
  - All leaves are at the same level
- Internal nodes store key values which guide searching in the tree
  - An internal node has between ceil(M/2) and M children (inclusive)
    - The root can have between 2 and M children
  - Internal node holds one fewer keys than it has children
    - Leftmost child has no key stored in it
    - Every other child has a key stored in it which is equal to the smallest key in the 
      subtree rooted at that child

### Designing a B tree ###

- Suppose each key takes K bytes, each pointer to a child node takes P bytes
  - Each internal node must be able to hold M * P + ( M - 1 ) * K bytes
- Suppose each data record takes R bytes
  - Each leaf node must be able to hold R bytes
- If each disk block contains B bytes, you should make M and L as large as possible while 
  satisfying the above inequalities. If B < R, then mulitple blocks must be used for each 
  leaf
  - M < = ( B + K ) / ( P + K)
  - L < = B / R
- The branching factor is at least M/2, and there are at least L/2 records in each leaf node
- Therefore, if you are storing N data records, there will be at most 2N / L leaf nodes
- There are at most ( 2N / L ) / ( M / 2 ) nodes at the level above the leaves
- On a system w/ 32-bit int keys, 32-bit block pointers, 1024-byte blocks, 256-byte records
  - M = 128, L = 4
  - Height is at most log64 N 

### B-tree find ###

1. Read the keys from the root node into main memory
2. Do a serach amongst these keys to find which child to branch to
3. When visiting an internal node, read the keys from the disk
4. When you reach a leaf, read it into main memory and search for desired key

- Number of disk accesses = height of the tree
- Worst case time cost for find = O(log N)
- It's helpful to use different time units for disk access time cost

---

- Maximum time needed for a find: Td + Logm/2 N
- Maximum time needed to search within internal nodes during find: Tm * log2 M * logm/2 N
- Maximum time needed to search within leaf node during find: Tm * log2 L
- Therefore, total maxtime= Td * logm/2 N + Tm * log2 M + Tm * log2 L
- Disc accesses will dominate totla cost if Td/Tm is much greater than log2 M
- Optimize performance by speeding up disks and storing as much data in memory as possible

### B-tree insert ###

1. Descend the tree, finding where the node should be inserted.
2. If there is room, insert the new item there
3. Otherwise, split the leaf into two leaves, each one with an equal amount of data
4. If there is room in the parent, then add a new pointer to this leaf
5. Otherwise the internal node must be split into two internal nodes

### B-tree delete ###

1. Descend the tree, find the leaf that contains it
2. If the leaf has > ceil(L/2) data records, remove the record, making sure to update the 
   values in the ancestor nodes if neccesary
3. Try to borrow a node from one of the node's siblings
4. If that's not possible, destroy this node and redistribute the data to siblings
5. If this means that you'll need to propogate delete upwards, do so

### 2-3 Tree ###

- A B-tree with M=L=3 is a 2-3-Tree
- ceil(M/2) = 2, so each internal node has either 2 or 3 children
- each leaf has either 2 or 3 data records
- Not useful in disk database applications, but they are sometimes used for in-memory balanced
  trees because they have good performance
