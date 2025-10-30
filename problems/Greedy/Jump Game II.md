Leetcode 45 

Problem:
You are given an array nums where each element represents the max jump length from that position.

Goal:
Return the minimum number of jumps needed to reach the last index.

You are guaranteed that the end is reachable.

Greedy Intuition (Optimal — O(n))

We treat the problem like layered BFS, but implemented using greedy:

currentEnd → end of the current jump range

farthest → the farthest position reachable within the current range

Every time you move past currentEnd, you must make a jump, and update currentEnd = farthest.

This ensures minimum jumps, because you always take the jump that extends reach the most.

Example Walkthrough
Input:

[2,3,1,1,4]

i	nums[i]	farthest	currentEnd	jumps
0	2	2	0 → 2	1
1	3	4	—	—
2	1	4	2 → 4	2

✅ Reached end
✅ Minimum jumps = 2

                                    class Solution {
                                        public int jump(int[] nums) {
                                            int jumps = 0;
                                            int currentEnd = 0;
                                            int farthest = 0;

                                            for (int i = 0; i < nums.length - 1; i++) {
                                                farthest = Math.max(farthest, i + nums[i]);

                                                if (i == currentEnd) {    // must make a jump
                                                    jumps++;
                                                    currentEnd = farthest;
                                                }
                                            }

                                            return jumps;
                                        }
                                    }

| Complexity | Value |
| ---------- | ----- |
| **Time**   | O(n)  |
| **Space**  | O(1)  |

