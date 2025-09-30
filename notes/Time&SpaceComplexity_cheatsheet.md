📘 Time & Space Complexity Cheat Sheet

🔹 Common Complexities

| Complexity     | Name        | Example                                         |
| -------------- | ----------- | ----------------------------------------------- |
| **O(1)**       | Constant    | Accessing array element, simple math operations |
| **O(log n)**   | Logarithmic | Binary Search, tree height traversal            |
| **O(n)**       | Linear      | Linear Search, traversing an array              |
| **O(n log n)** | Log-linear  | Merge Sort, Quick Sort (avg case), Heap Sort    |
| **O(n²)**      | Quadratic   | Bubble Sort, Insertion Sort, Selection Sort     |
| **O(2ⁿ)**      | Exponential | Recursive Fibonacci, Subset generation          |
| **O(n!)**      | Factorial   | Travelling Salesman (brute force), permutations |


🔹 Searching Algorithms

| Algorithm     | Time Complexity | Space Complexity |
| ------------- | --------------- | ---------------- |
| Linear Search | O(n)            | O(1)             |
| Binary Search | O(log n)        | O(1)             |

🔹 Sorting Algorithms

| Algorithm      | Best       | Average    | Worst      | Space            |
| -------------- | ---------- | ---------- | ---------- | ---------------- |
| Bubble Sort    | O(n)       | O(n²)      | O(n²)      | O(1)             |
| Selection Sort | O(n²)      | O(n²)      | O(n²)      | O(1)             |
| Insertion Sort | O(n)       | O(n²)      | O(n²)      | O(1)             |
| Merge Sort     | O(n log n) | O(n log n) | O(n log n) | O(n)             |
| Quick Sort     | O(n log n) | O(n log n) | O(n²)      | O(log n) (stack) |
| Heap Sort      | O(n log n) | O(n log n) | O(n log n) | O(1)             |

🔹 Data Structures

| Data Structure                | Access   | Search               | Insert   | Delete   | Space |
| ----------------------------- | -------- | -------------------- | -------- | -------- | ----- |
| Array                         | O(1)     | O(n)                 | O(n)     | O(n)     | O(n)  |
| Hash Table                    | –        | O(1) avg, O(n) worst | O(1)     | O(1)     | O(n)  |
| Stack / Queue                 | O(n)     | O(n)                 | O(1)     | O(1)     | O(n)  |
| Binary Search Tree            | O(log n) | O(log n)             | O(log n) | O(log n) | O(n)  |
| Balanced BST (AVL, Red-Black) | O(log n) | O(log n)             | O(log n) | O(log n) | O(n)  |

🔹 Recursion & DP

| Problem           | Time  | Space (stack/memo) |
| ----------------- | ----- | ------------------ |
| Factorial (rec)   | O(n)  | O(n)               |
| Fibonacci (naive) | O(2ⁿ) | O(n)               |
| Fibonacci (DP)    | O(n)  | O(n) or O(1)       |
| Matrix Chain Mult | O(n³) | O(n²)              |



⚡ Tips to Master Complexity Analysis

1. Count loops → each adds a factor (O(n), nested → multiply).

2. Consider recursion depth → adds stack space.

3. Ignore constants and low-order terms → Big-O focuses on growth.

4. Always think of worst-case unless specified.