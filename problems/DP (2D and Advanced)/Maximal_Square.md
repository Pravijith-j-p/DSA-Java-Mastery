Leetcode 221

Problem : 
Given an m x n binary matrix filled with '0' and '1', find the largest sqaure containing only 1's and return its area.

Example 1:

Input : 

matrix = [
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]

Output:
4

Explanation: The largest square has side length 2 → area = 2*2 = 4.

🔹 Example 2

Input:

matrix = [["0","1"],["1","0"]]


Output:
1

⚙️ Approach — Dynamic Programming

Let’s define a DP table:

dp[i][j] = side length of the largest square whose **bottom-right corner** is at (i, j)

🧠 Recurrence

If matrix[i][j] == '1':

dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])


Why?
The largest square ending at (i,j) depends on the minimum of the squares ending at its top, left, and top-left neighbors.

If matrix[i][j] == '0':

dp[i][j] = 0

🧱 Base Case

For first row or first column:

dp[i][0] = matrix[i][0] - '0'
dp[0][j] = matrix[0][j] - '0'

                                class Solution {
                                    public int maximalSquare(char[][] matrix) {
                                        if (matrix.length == 0) return 0;
                                        int m = matrix.length;
                                        int n = matrix[0].length;
                                        int[][] dp = new int[m][n];
                                        int maxSide = 0;

                                        for (int i = 0; i < m; i++) {
                                            for (int j = 0; j < n; j++) {
                                                if (matrix[i][j] == '1') {
                                                    if (i == 0 || j == 0) {
                                                        dp[i][j] = 1;
                                                    } else {
                                                        dp[i][j] = 1 + Math.min(dp[i-1][j-1],
                                                                        Math.min(dp[i-1][j], dp[i][j-1]));
                                                    }
                                                    maxSide = Math.max(maxSide, dp[i][j]);
                                                }
                                            }
                                        }

                                        return maxSide * maxSide; // area
                                    }
                                }
Time complexity : O(m x n)
Space complexity : O(m x n)

