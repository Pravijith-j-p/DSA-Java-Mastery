Leetcode 56

Problem : 

Merge Intervals — Intuition

You are given a list of intervals:

Some may overlap.

Goal → merge all overlapping intervals and return a list of non-overlapping, sorted intervals.

✅ Key Insight

If intervals are sorted by start time, we can merge them in a single sweep.

Two intervals overlap if:

current.start <= last.end


If they overlap → merge:

last.end = max(last.end, current.end)


If not → add the interval separately.

✅ Steps

1️⃣ Sort intervals by start time
2️⃣ Use result list and iterate
3️⃣ Merge overlapping intervals
4️⃣ Add non-overlapping ones

Example

Input:

[[1,3],[2,6],[8,10],[15,18]]

Process:

Merge [1,3] & [2,6] → [1,6]

No overlap: [8,10]

No overlap: [15,18]

Output:

[[1,6],[8,10],[15,18]]

                        class Solution {
                            public int[][] merge(int[][] intervals) {
                                if (intervals.length == 0) return new int[0][0];

                                // Step 1: Sort by start time
                                Arrays.sort(intervals, (a, b) -> a[0] - b[0]);

                                List<int[]> result = new ArrayList<>();
                                int[] current = intervals[0];
                                result.add(current);

                                // Step 2: Merge or add new interval
                                for (int[] interval : intervals) {
                                    int currentStart = current[0];
                                    int currentEnd = current[1];
                                    int nextStart = interval[0];
                                    int nextEnd = interval[1];

                                    if (nextStart <= currentEnd) {
                                        // Overlap → merge
                                        current[1] = Math.max(currentEnd, nextEnd);
                                    } else {
                                        // No overlap → add new interval
                                        current = interval;
                                        result.add(current);
                                    }
                                }

                                return result.toArray(new int[result.size()][]);
                            }
                        }

| Step         | Complexity     |
| ------------ | -------------- |
| Sorting      | O(n log n)     |
| Merging pass | O(n)           |
| Total Time   | **O(n log n)** |
| Space        | **O(n)**       |
