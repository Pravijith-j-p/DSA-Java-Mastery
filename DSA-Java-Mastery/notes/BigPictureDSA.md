
🚀 Big Picture: Data Structures & Algorithms

1️⃣ Data Structures (DS)

| Category    | Data Structure               | Usage                                  | Time Complexities (Common Ops)          |
| ----------- | ---------------------------- | -------------------------------------- | --------------------------------------- |
| **Linear**  | **Array**                    | Store fixed-size sequential data       | Access: O(1), Insert/Delete: O(n)       |
|             | **String**                   | Sequence of characters (special array) | Similar to array, + string-specific ops |
|             | **Linked List**              | Dynamic size, efficient insert/delete  | Insert/Delete: O(1), Access: O(n)       |
|             | **Stack**                    | LIFO (Last In First Out)               | Push/Pop: O(1)                          |
|             | **Queue**                    | FIFO (First In First Out)              | Enqueue/Dequeue: O(1)                   |
|             | **Deque**                    | Double-ended queue                     | Insert/Delete front & back: O(1)        |
| **Hashing** | **HashMap/HashSet**          | Key-value mapping / unique storage     | Avg O(1), worst O(n)                    |
| **Trees**   | **Binary Tree**              | Hierarchical data                      | Traversals: O(n)                        |
|             | **Binary Search Tree (BST)** | Sorted hierarchical                    | Search/Insert/Delete: O(log n)          |
|             | **Heap** (Priority Queue)    | Min/Max element quick access           | Insert/Delete: O(log n), Peek: O(1)     |
|             | **Trie**                     | Prefix-based search                    | Insert/Search: O(L) (L = word length)   |
| **Graphs**  | Adjacency List/Matrix        | Networks, relationships                | Traversals: O(V+E)                      |



2️⃣ Algorithms (Algo)

| Category                     | Algorithm                    | Usage                         | Time Complexity     |
| ---------------------------- | ---------------------------- | ----------------------------- | ------------------- |
| **Sorting**                  | Bubble, Insertion, Selection | Basic, small inputs           | O(n²)               |
|                              | Merge Sort, Quick Sort       | Divide & Conquer              | O(n log n)          |
|                              | Heap Sort                    | Priority queue                | O(n log n)          |
| **Searching**                | Linear Search                | Small arrays                  | O(n)                |
|                              | Binary Search                | Sorted arrays                 | O(log n)            |
| **Recursion & Backtracking** | DFS, N-Queens, Subsets       | Explore possibilities         | Exponential (worst) |
| **Dynamic Programming (DP)** | Knapsack, LIS, Matrix DP     | Optimal substructure problems | O(n²) to O(n³)      |
| **Greedy**                   | Interval scheduling, Huffman | Local choice → global optimum | O(n log n)          |
| **Graph Algorithms**         | BFS, DFS                     | Traversals                    | O(V+E)              |
|                              | Dijkstra, Bellman-Ford       | Shortest paths                | O(E log V), O(VE)   |
|                              | Kruskal, Prim                | Minimum Spanning Tree         | O(E log V)          |


3️⃣ MAANG Relevance

Arrays, Strings, Hashing, Binary Search → Most common in Coding Rounds.

Trees, Graphs, DP → Very frequent in Interviews.

Greedy + Advanced DS (Trie, Segment Tree, Union-Find) → Appear in hard problems.