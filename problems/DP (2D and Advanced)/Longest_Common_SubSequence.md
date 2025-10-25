Leetcode 1143

Given two strings text1 and text2, return the length of their longest common subsequence (LCS).

A subsequence of a string is a sequence derived by deleting some (or no) characters without changing the order of the remaining characters.

Example 1:

Input : 
text1 = "abcde" , text2= "ace"

Output:
3

Explanation : The LCS is "ace" -> length = 3

Example 2:
Input: text1 = "abc", text2= "abc"
Output : 3

Explanation : LCS = "abc"

⚙️ Approach — Dynamic Programming (Tabulation)

We’ll use a 2D DP array, where:
dp[i][j] = length of LCS between
text1[0..i-1] and text2[0..j-1]

🧠 Recurrence Relation

If last characters match:

dp[i][j] = 1 + dp[i-1][j-1]


If not:

dp[i][j] = max(dp[i-1][j], dp[i][j-1])


Base case:

dp[0][*] = 0 (empty string)

dp[*][0] = 0

                            class Solution {
                                public int longestCommonSubsequence(String text1, String text2) {
                                    int m = text1.length();
                                    int n = text2.length();
                                    int[][] dp = new int[m + 1][n + 1];

                                    for (int i = 1; i <= m; i++) {
                                        for (int j = 1; j <= n; j++) {
                                            if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                                                dp[i][j] = 1 + dp[i - 1][j - 1];
                                            } else {
                                                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                                            }
                                        }
                                    }

                                    return dp[m][n];
                                }
                            }
Time complexity : O(m x n)
Space complexity : O(m x n)

