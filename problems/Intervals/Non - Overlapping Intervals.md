Leetcode 435

Problem : 
You're given a set of intervals.
Goal:

✅ Remove the minimum number of intervals
✅ So that the rest of the intervals do not overlap

This is a classic Interval Scheduling Optimization problem.

Key Idea / Greedy Pattern

To minimize removals, we should:

✅ Keep intervals that end earliest
❌ because early-ending intervals leave the most room for future intervals.

Greedy Strategy:

Sort intervals by end time

Always pick the interval that ends earliest

If the next interval overlaps, remove it

Overlap condition:

next.start < prev.end


If overlap → increment removals
Else → update prev = next

Example

Input:

[[1,2],[2,3],[3,4],[1,3]]


Sorted by end:

[1,2], [2,3], [1,3], [3,4]


Processing:

Pick [1,2]

[2,3] → OK (no overlap)

[1,3] → overlap → remove

[3,4] → OK

✅ Minimum removals = 1

                                class Solution {
                                    public int eraseOverlapIntervals(int[][] intervals) {
                                        if (intervals.length == 0) return 0;

                                        // Step 1: Sort by end time
                                        Arrays.sort(intervals, (a, b) -> a[1] - b[1]);

                                        int count = 0;
                                        int prevEnd = intervals[0][1];

                                        // Step 2: Greedily remove overlapping intervals
                                        for (int i = 1; i < intervals.length; i++) {
                                            if (intervals[i][0] < prevEnd) {
                                                // Overlap → remove this interval
                                                count++;
                                            } else {
                                                // No overlap → keep it and update end
                                                prevEnd = intervals[i][1];
                                            }
                                        }

                                        return count;
                                    }
                                }

| Operation    | Complexity     |
| ------------ | -------------- |
| Sorting      | O(n log n)     |
| Greedy sweep | O(n)           |
| **Total**    | **O(n log n)** |
| Space        | **O(1)**       |
