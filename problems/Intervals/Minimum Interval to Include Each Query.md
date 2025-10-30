Leetcode 1851

Problem : 
You’re given:

intervals = [[l1, r1], [l2, r2], ...]

queries = [q1, q2, ...]

For each query qi, find the length of the smallest interval (r - l + 1) that contains qi.
If no interval contains the query → return -1.

✅ Intuition

We need the minimum interval that covers each query.

If we process intervals in arbitrary order → too slow.
Instead, use a smart ordering + min-heap.

🧠 Key Ideas

Sort intervals by start

Sort queries in increasing order

Use a min-heap that stores only intervals that can cover the current query

Remove intervals whose end < query (cannot cover anymore)

The heap’s top gives smallest interval length covering query

This avoids checking every interval for every query → optimal.

✅ Approach (Optimal)
✅ Step-by-step

Sort intervals by start

Sort queries while keeping original index

Use a min-heap storing

[interval_length, end]


For each query:

Add all intervals whose start <= query

Remove from heap all intervals whose end < query

The top of the heap now has the valid smallest interval

Store results according to original query order

Example

Intervals:

[[1,4], [2,4], [3,6], [4,4]]


Queries:

[2,3,4,5]


Output:

[3,3,1,4]

                                class Solution {
                                    public int[] minInterval(int[][] intervals, int[] queries) {
                                        // Sort intervals by starting point
                                        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);

                                        // Pair each query with its index
                                        int n = queries.length;
                                        int[][] queryWithIndex = new int[n][2];
                                        for (int i = 0; i < n; i++) {
                                            queryWithIndex[i][0] = queries[i];
                                            queryWithIndex[i][1] = i;
                                        }
                                        
                                        // Sort queries
                                        Arrays.sort(queryWithIndex, (a, b) -> a[0] - b[0]);

                                        // Min-heap → stores {interval_length, end}
                                        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);

                                        int[] result = new int[n];
                                        int i = 0;

                                        for (int[] qi : queryWithIndex) {
                                            int q = qi[0];
                                            int idx = qi[1];

                                            // Add all intervals whose start <= q
                                            while (i < intervals.length && intervals[i][0] <= q) {
                                                int start = intervals[i][0];
                                                int end = intervals[i][1];
                                                int length = end - start + 1;
                                                pq.add(new int[] { length, end });
                                                i++;
                                            }

                                            // Remove intervals that cannot include q
                                            while (!pq.isEmpty() && pq.peek()[1] < q) {
                                                pq.poll();
                                            }

                                            // Find smallest valid interval
                                            result[idx] = pq.isEmpty() ? -1 : pq.peek()[0];
                                        }

                                        return result;
                                    }
                                }

Time: O((n + q) log n)
Space: O(n)