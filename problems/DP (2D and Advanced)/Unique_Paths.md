Leetcode 62

Problem : 
You are given a grid with m rows and n columns.
You are a robit starting at the top-left corner (0,0) and your goal is to reach bottom-right corner(m - 1, n - 1)

At any point , you can only move

- Down or
- Right

Find the number of unique paths you can take to reach the destination

Example :
Input : 
m = 3, n = 7

Output : 28

Explanation : There are 28 possible unique paths to reach the bottom-right corner

Approach 1 - Dynamic Programming (Tabulation)

The Idea:
- if you are at (i,j), you could have come either from the top (i-1, j) or from the left (i, j-1).

So,

dp[i][j] = dp[i-1][j] + dp[i][j-1]


Base case:

There is only 1 way to reach any cell in the first row (all right moves)

Similarly, 1 way to reach any cell in the first column (all down moves)

                            class Solution {
                                public int uniquePaths(int m, int n) {
                                    int[][] dp = new int[m][n];

                                    // Initialize first row and first column
                                    for (int i = 0; i < m; i++)
                                        dp[i][0] = 1;
                                    for (int j = 0; j < n; j++)
                                        dp[0][j] = 1;

                                    // Fill the DP table
                                    for (int i = 1; i < m; i++) {
                                        for (int j = 1; j < n; j++) {
                                            dp[i][j] = dp[i-1][j] + dp[i][j-1];
                                        }
                                    }

                                    return dp[m-1][n-1];
                                }
                            }
Time Complexity : O(m * n)
Space Complexity : O(m * n)

