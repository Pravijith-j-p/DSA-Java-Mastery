Leetcode 253

Problem : 
You are given an array of meeting intervals where each interval is [start, end].
Determine whether a person can attend all meetings — i.e., no intervals should overlap.

Example:
Input: [[0,30],[5,10],[15,20]]
Output: false

✅ Intuition

If two meetings overlap, a person cannot attend both.

🧠 Key idea:
Sort the intervals by start time → if any meeting starts before the previous one ends, it is impossible.

✅ Approach

Sort intervals by start time

Iterate through them

If current.start < previous.end → Overlap → return false

If loop completes → return true

Example

Input:

[[7,10],[2,4]]


Sorted:

[[2,4],[7,10]]


No overlap → ✅ You can attend all meetings

                                class Solution {
                                    public boolean canAttendMeetings(int[][] intervals) {
                                        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);

                                        for (int i = 1; i < intervals.length; i++) {
                                            if (intervals[i][0] < intervals[i - 1][1]) {
                                                return false; // overlap
                                            }
                                        }
                                        return true;
                                    }
                                }

Time: O(n log n) due to sorting

Space: O(1) (in-place sorting)