A priority Queue is an abstract data structure similar to regular queue, but with priorities assigned to elements
- Higer priority elements are served before lower priority elements, regardless if insertion order.
- it doesn't strictly follow FIFO - order depends on priority

⚡ Key Characteristics

| Feature        | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| Ordering       | Elements are ordered by **priority**                         |
| Root           | Always contains the **highest (or lowest) priority element** |
| Implementation | Usually with **heap** (min-heap or max-heap)                 |
| Insertion      | Adds element based on **priority**                           |
| Deletion       | Removes the **highest-priority element** first               |

🔹 How It Works Internally
- Internally implemented using a heap (complete binary tree).

- Insertion → element added at the end → heapify up to maintain heap property.

- Removal → root element removed → heapify down to restore heap property.

