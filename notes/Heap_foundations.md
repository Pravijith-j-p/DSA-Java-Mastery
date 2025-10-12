A Heap is a complete bonary tree that satisfies the heap property:
- In a Max Heap, every parent node is greater than or equal to it's children
- In a Min Heap, every parent node is smaller than or equal to its children

This means:
The root node always contains the maximum (for Max Heap) or minimum(for Min Heap) element

🌳 Structure

A Heap is :
- Complete Binary Tree -> all levels are completely filled except possibly the last, which is filled from left to right
- stored as an array, not as a linked tree

Example : Min Heap 
                                             1
                                            / \
                                           3   5
                                          /\   /
                                         4  8  6

                                     Array Representation = [1, 3, 5, 4, 8, 6]

 ⚙️ Heap Operations

 | Operation                       | Description                                        | Time Complexity |
| ------------------------------- | -------------------------------------------------- | --------------- |
| `insert(x)`                     | Adds a new element while maintaining heap property | O(log n)        |
| `extractMin()` / `extractMax()` | Removes root (min or max) and restores heap        | O(log n)        |
| `peek()`                        | Returns root (min or max) without removing         | O(1)            |
| `heapify()`                     | Converts an array into a heap                      | O(n)            |

 Example (Min Heap)

                        import java.utils.*;

                        public class MinHeapExample{
                            public static void main(String [] args){
                                PriorityQueue<Integer> minHeap = new PriorityQueue<>();

                                //Insert elements
                                minHeap.add(10);
                                minHeap.add(5);
                                minHeap.add(20);
                                minHeap.add(3);

                                //Peek top(smallest)
                                System.out.println(minHeap.peek());

                                //remove elements
                                while(!minHeap.isEmpty()){
                                    System.out.print(minHeap.poll()+ " ");
                                }
                            }
                        }

Example (Max Heap)
 
                        import java.util.*

                        public class MaxHeapExample{
                            public static void main(String [] args){
                                PriorityQueue <Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

                                maxHeap.add(10);
                                maxHeap.add(5);
                                maxHeap.add(20);
                                maxHeap.add(3);

                                while(!maxHeap.isEmpty()){
                                    System.out.print(maxHeap.poll() + " ");
                                }
                            }
                        }

🔄 Internal Representation (Array Indexing)

For a node at index i in an array:

| Relation    | Formula       |
| ----------- | ------------- |
| Left Child  | `2 * i + 1`   |
| Right Child | `2 * i + 2`   |
| Parent      | `(i - 1) / 2` |


