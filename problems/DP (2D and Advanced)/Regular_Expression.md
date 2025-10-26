Leetcode 10

Problem :
Given an input string s and a pattern p, implement regular expression matching with support for:
- . -> Mathches any single character
- * -> Matches zero or more of the preceding element

Return true if the pattern matches the entire string

Example 1:
Input :
s = "aa" , p = "a"
Output : false
Explanation : "a" does not match the entire string "aa"

Input: s = "aa", p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, so 'a*' matches "aa".

Input: s = "ab", p = ".*"
Output: true
Explanation: ".*" means "zero or more of any character".



🧠 Intuition
We can’t use greedy matching here — it’s Dynamic Programming because we must consider overlapping subproblems.

Let’s define a DP table:

sql
Copy code
dp[i][j] = true if s[0..i-1] matches p[0..j-1]
Base Case
dp[0][0] = true → Empty string matches empty pattern.

dp[0][j] → Only true if the pattern can represent an empty string
(i.e., like a*, a*b*, etc.)

Transition
1️⃣ If current pattern character is NOT *
Match must be direct or .

java
Copy code
if (p[j - 1] == s[i - 1] || p[j - 1] == '.') {
    dp[i][j] = dp[i - 1][j - 1];
}
2️⃣ If current pattern character IS *
Two possibilities:

* counts as zero of the preceding char
→ dp[i][j] = dp[i][j - 2]

* counts as one or more of the preceding char
→ if previous pattern char matches s[i-1]

java
Copy code
if (s[i - 1] == p[j - 2] || p[j - 2] == '.') {
    dp[i][j] = dp[i - 1][j];
}

                                class Solution {
                                    public boolean isMatch(String s, String p) {
                                        int m = s.length(), n = p.length();
                                        boolean[][] dp = new boolean[m + 1][n + 1];

                                        dp[0][0] = true;

                                        // Handle patterns like a*, a*b*, a*b*c* at the beginning
                                        for (int j = 2; j <= n; j++) {
                                            if (p.charAt(j - 1) == '*') {
                                                dp[0][j] = dp[0][j - 2];
                                            }
                                        }

                                        for (int i = 1; i <= m; i++) {
                                            for (int j = 1; j <= n; j++) {
                                                char sc = s.charAt(i - 1);
                                                char pc = p.charAt(j - 1);

                                                if (pc == sc || pc == '.') {
                                                    dp[i][j] = dp[i - 1][j - 1];
                                                } else if (pc == '*') {
                                                    dp[i][j] = dp[i][j - 2]; // zero occurrence

                                                    char prev = p.charAt(j - 2);
                                                    if (prev == sc || prev == '.') {
                                                        dp[i][j] = dp[i][j] || dp[i - 1][j];
                                                    }
                                                }
                                            }
                                        }

                                        return dp[m][n];
                                    }
                                }

Time complexity : O(m x n)
Space Complexity : O(m x n)
