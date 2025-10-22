Leetcode 213

Problem :
You are a professional robber planning to rob houses along a circular street.
Each house has some amount of money stashed, but adjacent houses have security systems connected.

The first and last houses are also adjacent because of the circular arrangement.

Return the maximum amount of money you can rob without robbing two adjacent houses.

Example 1 :
Input : 
nums = [2, 3, 2]

Output : 
3

Explanation : 
You cannot rob house 1 and 3 because they are adjacent
So best is rob house 2

Example 2:
nums = [1, 2, 3, 1]
Output : 
4

                                class Solution {
                                    public int rob(int[] nums) {
                                        int n = nums.length;
                                        if (n == 1) return nums[0];
                                        if (n == 2) return Math.max(nums[0], nums[1]);

                                        return Math.max(robRange(nums, 0, n - 2), robRange(nums, 1, n - 1));
                                    }

                                    private int robRange(int[] nums, int start, int end) {
                                        int prev1 = 0; // dp[i-1]
                                        int prev2 = 0; // dp[i-2]
                                        
                                        for (int i = start; i <= end; i++) {
                                            int temp = prev1;
                                            prev1 = Math.max(prev1, prev2 + nums[i]);
                                            prev2 = temp;
                                        }

                                        return prev1;
                                    }
                                }

                               