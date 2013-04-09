# Lecture 14 #
<br />

### Connected Graph (undirected) ###
There is a path from each vertex to every other vertex

### Strongly Connected Graph (directed) ###
There is a path from each vertex to every other vertex

### Weakly Connected Graph (directed) ###
Graph is not strongly connected, but the underlying undirected graph is connected

### Completely Connected Graph ###
There is an edge from each vertex to every other vertex

Spanning Trees
--------------

A tree of an undirected graph G is an undirected graph that:

- Contains all vertices of G
- Contains only edges of G
- No cycles
- Connected

---

- Only connected graphs have spanning trees
- Any vertex could be the root
- You can use bfs to find a spanning tree in an unweighted graph
- O(|V| + |E|)

### Prim's Algorithm ###

- Modification of Djikstra's
- Same time complexity: O(|E| log |V|)

---

1. Pick an arbitrary start vertex, s
2. Add the edges to a priority queue
3. If the priority queue is empty, you are done
4. Remove the edge with the smallest cost from the queue
5. If the 'done' field for the end vertex true, goto 3
6. Mark 'done' for the end vertex, set prev for 'w' as 'v'
7. Put each edge from the end vertex into the priority queue
8. Goto 3

### Kruskal's algorithm ###

- Builds's a bottom-up MST

---

1. Create a forest of 1 node trees
2. Create a priority queue that contains all of the edges in E
3. While < V - 1 edges have been added
  1. Delete the smallest-weight edge from the priority queue
  2. If the two vertices in the edge are in the same forest, don't use it
  3. Otherwise join the vertices with that edge

