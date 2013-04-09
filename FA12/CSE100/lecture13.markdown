Lecture 13
----------

## Unweighted Shortest Path ##
- It's a bfs

- Give all vertices in graph a distance of infinity
- Start @ s, give s distance 0
- Enqueue s into a queue
- While the queue is not empty
  - Dequeue the vertex v,
  - For each of v's adjacent nodes that haven't been visited
  - Set distance as 1 + distance to v
  - Enqueue

Djikstra's Algorithm Complexity: O(|E| log |E|) / O(|V|^2log|E|) / O(|E| log|V|)
