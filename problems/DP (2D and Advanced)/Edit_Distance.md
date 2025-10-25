Leetcode 72

Problem : 
Given two strings word1 and word2 , return the minimum number of operatiobs required to convert word1 to word2

You can perform three operations :
- Insert a character
- Delete a character
- Replace a charcter

Example 1:
Input : word1 = "horse", word2 = "ros"

Output : 3

Explanation : 
horse -> rorse (replace h with r)
rorse -> rose (remove r)
rose -> ros (remove e)

Example 2
Input : word1 = "intention", word2 = "execution"

Output : 5
Explanation : 
intention → inention (remove 't')
inention  → enention (replace 'i' with 'e')
enention  → exention (replace 'n' with 'x')
exention  → exection (replace 'n' with 'c')
exection  → execution (insert 'u')

⚙️ Intuition

We’ll use Dynamic Programming.

Let dp[i][j] represent the minimum number of operations to convert
word1[0..i-1] → word2[0..j-1].

🧠 Recurrence Relation

If characters match:

dp[i][j] = dp[i-1][j-1]


If not match:
We consider the 3 possible operations:

Insert: dp[i][j-1] + 1

Delete: dp[i-1][j] + 1

Replace: dp[i-1][j-1] + 1

So:

dp[i][j] = 1 + min(
    dp[i-1][j],    // delete
    dp[i][j-1],    // insert
    dp[i-1][j-1]   // replace
)

🧱 Base Case

If one string is empty:

Converting empty string to length j requires j inserts

Converting length i to empty string requires i deletes

So:

dp[0][j] = j
dp[i][0] = i

                            class Solution {
                                public int minDistance(String word1, String word2) {
                                    int m = word1.length();
                                    int n = word2.length();
                                    int[][] dp = new int[m + 1][n + 1];

                                    // Base cases
                                    for (int i = 0; i <= m; i++) dp[i][0] = i;
                                    for (int j = 0; j <= n; j++) dp[0][j] = j;

                                    // Fill DP table
                                    for (int i = 1; i <= m; i++) {
                                        for (int j = 1; j <= n; j++) {
                                            if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                                                dp[i][j] = dp[i - 1][j - 1];
                                            } else {
                                                dp[i][j] = 1 + Math.min(
                                                    dp[i - 1][j],                 // Delete
                                                    Math.min(dp[i][j - 1],        // Insert
                                                            dp[i - 1][j - 1])    // Replace
                                                );
                                            }
                                        }
                                    }

                                    return dp[m][n];
                                }
                            }
Time complexity : O(m x n)
Space complexity : O(m x n)

