Leetcode 57

✅ Insert Interval — Intuition

You're given:

A list of non-overlapping, sorted intervals.

A new interval to insert.

Goal:

✅ Insert the new interval
✅ Merge overlaps
✅ Maintain sorted, non-overlapping structure

✅ Key Idea / Pattern: Merge Intervals

We follow a three-phase sweep:

✅ 1. Add intervals completely before newInterval

These intervals end before the newInterval starts:

interval.end < new.start


→ Add as-is.

✅ 2. Merge overlapping intervals

These intervals overlap with newInterval if:

interval.start <= new.end


→ Expand the new interval:

new.start = min(new.start, interval.start)
new.end   = max(new.end, interval.end)

✅ 3. Add intervals completely after newInterval

These start after newInterval ends:

interval.start > new.end


→ Add as-is.

✅ Example
intervals:
[ [1,3], [6,9] ]


newInterval: [2,5]

Process

Before new: [1,3] overlaps → merged → [1,5]

Add merged

Add [6,9]

✅ Final:

[[1,5], [6,9]]


                            class Solution {
                                public int[][] insert(int[][] intervals, int[] newInterval) {
                                    List<int[]> result = new ArrayList<>();

                                    int i = 0;
                                    int n = intervals.length;

                                    // 1. Add all intervals before newInterval
                                    while (i < n && intervals[i][1] < newInterval[0]) {
                                        result.add(intervals[i]);
                                        i++;
                                    }

                                    // 2. Merge all overlapping intervals
                                    while (i < n && intervals[i][0] <= newInterval[1]) {
                                        newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
                                        newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
                                        i++;
                                    }

                                    // Add merged new interval
                                    result.add(newInterval);

                                    // 3. Add the remaining intervals
                                    while (i < n) {
                                        result.add(intervals[i]);
                                        i++;
                                    }

                                    return result.toArray(new int[result.size()][]);
                                }
                            }

| Operation     | Complexity |
| ------------- | ---------- |
| Sweep & merge | **O(n)**   |
| Space         | **O(n)**   |
