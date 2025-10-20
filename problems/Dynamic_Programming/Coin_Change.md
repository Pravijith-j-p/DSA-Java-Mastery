Leetcode 322

Problem : 
Given an integer array coins representing different denominations and an integer amount representing a total amount of money

Return the fewest number of coins needed to make up that amount
If that amount cannot be made up by any combination of the coins, return -1

Example:
Input:'coins = [1, 2, 5] , amount = 11

Output 
3
Explanation:
11 = 5 + 5 + 1      -> 3 coins

Example 2:

coins [2] , amount = 3

Output : -1

💡 Intution
At each amount i, we can take one coin c and see
 - If we take coin c, then we need to solve the subproblem for i-c
 - So, the recurrance relation is:
 dp[i] = min(dp[i], dp[i-c] + 1)
 where dp[i] is the minimum number of coins needed for amount i.

 Optimal Solution

                            class Solution{
                                public int coinChange(int []coins, int amount){
                                    int[] dp = new int [amount+1];
                                    Arrays.fill(dp, amount + 1);        //Initialize with large value (infinity)
                                    dp[0] = 0;      //0 coins to make amount 0

                                    for(int i = 1;i<= amount; i++){
                                        for(int coin: coins){
                                            if( i - coin >= 0){
                                                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                                            }
                                        }
                                    }
                                    return dp[amount] > amount ? -1 : dp[amount];
                                }
                            }
Time : O(n x amount)
Space : O(amount)