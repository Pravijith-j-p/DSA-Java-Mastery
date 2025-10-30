Leetcode 55

Problem :
You are given an array nums where each nums[i] tells how far you can jump from index i.

Goal:
Return true if you can reach the last index, else false.

✅ Greedy Intuition

Keep track of the farthest index you can reach.

While scanning the array:

If at any index i, you find that i > farthest → you are stuck → return false.

Otherwise, update:

farthest = max(farthest, i + nums[i])


If farthest >= last index, return true.

This works because you always want the jump that gives the farthest reach.

Example Walkthrough
Input:

[2,3,1,1,4]

i	nums[i]	farthest before	farthest after
0	2	0	2
1	3	2	4 ✅ reaches end

Output : true

                                    class Solution {
                                        public boolean canJump(int[] nums) {
                                            int farthest = 0;

                                            for (int i = 0; i < nums.length; i++) {
                                                if (i > farthest) return false;      // stuck
                                                farthest = Math.max(farthest, i + nums[i]);
                                            }

                                            return true;
                                        }
                                    }

| Complexity | Value |
| ---------- | ----- |
| **Time**   | O(n)  |
| **Space**  | O(1)  |

