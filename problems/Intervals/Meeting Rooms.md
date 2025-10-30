Leetcode 252

Problem : 
You are given an array of meeting intervals:

[[start1, end1], [start2, end2], ...]


Goal:

✅ Return true if a person can attend all meetings
❌ Return false if any meeting overlaps

✅ Key Insight / Pattern

This is a simple interval overlap check.

🧠 Overlap occurs when:
current.start < previous.end


So the steps are:

Sort intervals by start time

Compare each interval with the previous one

If any overlap → return false

Otherwise → true

Example
Input:
[[0,30],[5,10],[15,20]]


Sorted:

[0,30]
[5,10]   ← starts before 30 → overlap ✅


Output:

false

Input:
[[7,10],[2,4]]


Sorted:

[2,4]
[7,10]  ← no overlap


Output:

true


                                        class Solution {
                                            public boolean canAttendMeetings(int[][] intervals) {
                                                if (intervals.length == 0) return true;

                                                // Step 1: Sort by start time
                                                Arrays.sort(intervals, (a, b) -> a[0] - b[0]);

                                                // Step 2: Check for overlap
                                                for (int i = 1; i < intervals.length; i++) {
                                                    if (intervals[i][0] < intervals[i - 1][1]) {
                                                        // Overlap found
                                                        return false;
                                                    }
                                                }

                                                return true;
                                            }
                                        }

| Step  | Complexity       |
| ----- | ---------------- |
| Sort  | **O(n log n)**   |
| Scan  | **O(n)**         |
| Total | ✅ **O(n log n)** |
| Space | **O(1)**         |
