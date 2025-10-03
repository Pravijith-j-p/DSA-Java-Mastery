A linked list is a linear data structure where elements (called nodes) are connected using pointers

Each node contains :
- Data -> the value
- Pointer -> reference to the next node

Variants:
1. Single linked List -> nodes point only to the next node
2. Doubly Linked List -> nodes have pointers to both next and previous node
3. Circular Linked List -> last node points back to head

Comparison with Arrays
| Feature            | Array                  | Linked List                     |
| ------------------ | ---------------------- | ------------------------------- |
| Memory             | Contiguous             | Non-contiguous (dynamic)        |
| Access (random)    | O(1)                   | O(n)                            |
| Insertion/Deletion | O(n) (shifting needed) | O(1) if node reference is known |
| Cache friendly     | ✅ Yes                  | ❌ No                            |

1. Two-Pointer / Fast & Slow Pointer

Used for detecting cycles, finding middle, etc.
Pattern idea: Move one pointer (slow) step by step, and another (fast) two steps.

Common problems:

Detect cycle in linked list (Floyd’s Cycle Detection).

Find the middle node.

Find the nth node from end.

Check if linked list is a palindrome.

2. Reversal Pattern

Reversing a linked list or a part of it is very common.
Techniques:

Iterative reversal with three pointers (prev, curr, next).

Recursive reversal.

Common problems:

Reverse a linked list.

Reverse a sublist (between m and n).

Reverse nodes in k-groups.

Rotate linked list.

3. Merge Pattern

Often appears when dealing with sorted lists.

Common problems:

Merge two sorted linked lists.

Merge k sorted linked lists (use Min-Heap or Divide & Conquer).

Sort a linked list (Merge Sort).

4. Cycle / Loop Detection

Detect if a cycle exists.

Find the node where cycle begins.

Technique: Floyd’s cycle detection (fast/slow pointers).

5. Dummy Node Pattern

Use a dummy node to simplify edge cases when manipulating the head.
Very common in:

Adding two numbers (Linked List representation).

Removing Nth node from end.

Partitioning a linked list around a value.

6. Recursive Linked List Problems

Linked Lists naturally lend themselves to recursion.

Reverse a list recursively.

Merge two sorted lists recursively.

Check palindrome recursively.

🏆 Frequently Asked MAANG Linked List Questions

- Reverse Linked List (LeetCode 206)

- Merge Two Sorted Lists (21)

- Linked List Cycle (141) & Cycle II (142)

- Remove Nth Node From End (19)

- Reorder List (143)

- Palindrome Linked List (234)

- Add Two Numbers (2)

- Copy List with Random Pointer (138)

- Intersection of Two Linked Lists (160)

- Merge K Sorted Lists (23)

- Sort List (148)

- Rotate List (61)