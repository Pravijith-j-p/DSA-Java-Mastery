Leetcode 416 :

Problem : 
Given an integer array nums
Return true if yiu can partition the array into two subsets such that the sum of elements on both subsets is equal, otherwise return false.

Example1:
Input : 
nums = [1, 5, 11, 5]

Output : 
true

Explanation : 
The array can be partitioned as :
- [1, 5, 5] and [11]
- Both have sum = 11

Example 2 :
Input : 
nums = [1, 2, 3, 5]
Output : 
false

Explanation :
No partition possible with equal subset sums

💡 Intuition

This is a Subset Sum Problem in disguise.

Let the total sum = S.

We want two subsets with equal sum → each subset must sum to S / 2.

So the problem becomes:

“Is there a subset of nums that sums to S / 2?”

⚠️ Early Check

If S is odd, you can immediately return false.
Because you can’t split an odd number evenly.

🧠 Dynamic Programming Idea

We’ll use a boolean DP array:

dp[i][j] → whether we can make sum j using the first i elements.

🧩 Transition

For each number nums[i]:

dp[i][j] = dp[i-1][j] || dp[i-1][j - nums[i]]  if j >= nums[i]
otherwise dp[i][j] = dp[i-1][j]


Meaning:

You can either exclude the number, or

Include it (if it fits into the target).

🏁 Base Case

dp[0][0] = true (Sum 0 is always possible — take nothing)

dp[i][0] = true for all i

dp[0][j] = false for all j > 0

                                    class Solution {
                                        public boolean canPartition(int[] nums) {
                                            int sum = 0;
                                            for (int num : nums) sum += num;
                                            if (sum % 2 != 0) return false;

                                            int target = sum / 2;
                                            boolean[] dp = new boolean[target + 1];
                                            dp[0] = true;

                                            for (int num : nums) {
                                                // Iterate backwards to avoid overwriting current row
                                                for (int j = target; j >= num; j--) {
                                                    dp[j] = dp[j] || dp[j - num];
                                                }
                                            }

                                            return dp[target];
                                        }
                                    }

