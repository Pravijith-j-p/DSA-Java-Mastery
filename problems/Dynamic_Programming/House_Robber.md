Leetcode 198

Problem : 
You are a professional robber planning to rob houses along a street
Each house has a certain amount of money stashed , but adjacent houses have security systems connected - 
if you rob two adjacent houses, you get caught
Return maximum amount of money you can rob without getting caught

Example 1
Input 
nums = [1, 2, 3, 1]
Output : 4
Explanation:
Rob House 1 (1) and house 3 (3) -> 1 + 3 = 4

Example 2
nums = [2, 7, 9, 3, 1]

Output:
12

Explanation : 
Rob House 1 (2), house 3 (9), and house 5(1) -> 2 + 9 + 1 =12

Intution :
At every house i, you have two choices
1. Rob this house -> you can't rob house i - 1, but can add nums[i] to the profit up to i-2
2. Skip this house -> take profit from house i-1

So ,
dp[i] = max(dp[i - 1], nums[i] + dp [i - 2])
This is the core recurrence relation

Dynamic Programming

                            class Solution {
                                public int rob(int[] nums) {
                                    int n = nums.length;
                                    if (n == 0) return 0;
                                    if (n == 1) return nums[0];

                                    int[] dp = new int[n];
                                    dp[0] = nums[0];
                                    dp[1] = Math.max(nums[0], nums[1]);

                                    for (int i = 2; i < n; i++) {
                                        dp[i] = Math.max(dp[i - 1], nums[i] + dp[i - 2]);
                                    }

                                    return dp[n - 1];
                                }
                            }

                       
