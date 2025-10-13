Leetcode 295

Problem :
Design a data structure that :
- supports adding numbers from a stream (one by one)
- Return the median of all elements so far efficiently

You must implement two methods
void addNum(int num)
double findMedian()

Example :
addNum(1)
addNum(2)
findMedian() ->1.5
addNum(3)
findMedian() ->2

⚙️ We can maintain two Heaps:
1. Max-Heap (low-half) -> keeps the smaller half of numbers
2. Min-Heap (high-half) -> keeps larger half of numbers

Goal :
- both heaps are balanced (sizes differ at most by 1)
- All elements in max-heap <= all elements in min-heap

Then :
- If total count is odd -> median = root of larger heap
- if even -> median = average of both roots

🧮 Visualization Example

Let's insert: [1, 2, 3]

| Step | Operation | Max-Heap (low) | Min-Heap (high) | Median        |
| ---- | --------- | -------------- | --------------- | ------------- |
| 1    | addNum(1) | [1]            | []              | 1             |
| 2    | addNum(2) | [1]            | [2]             | (1+2)/2 = 1.5 |
| 3    | addNum(3) | [2,1]          | [3]             | 2             |

✅ The heaps stay balanced, and we can find the median in O(1).

                                    import java.util.*;

                                    class MedianFinder {
                                        private PriorityQueue<Integer> low;  // Max-heap
                                        private PriorityQueue<Integer> high; // Min-heap

                                        public MedianFinder() {
                                            // Max-heap for smaller half
                                            low = new PriorityQueue<>(Collections.reverseOrder());
                                            // Min-heap for larger half
                                            high = new PriorityQueue<>();
                                        }

                                        public void addNum(int num) {
                                            // Step 1: Add to max-heap first
                                            low.add(num);
                                            
                                            // Step 2: Ensure all elements in low <= high
                                            high.add(low.poll());

                                            // Step 3: Balance sizes (low can have 1 more element)
                                            if (low.size() < high.size()) {
                                                low.add(high.poll());
                                            }
                                        }

                                        public double findMedian() {
                                            if (low.size() > high.size()) {
                                                return low.peek(); // Odd count
                                            } else {
                                                return (low.peek() + high.peek()) / 2.0; // Even count
                                            }
                                        }
                                    }

| Operation      | Time     | Space |
| -------------- | -------- | ----- |
| `addNum()`     | O(log N) | O(N)  |
| `findMedian()` | O(1)     | O(N)  |


