Leetocde 91

Problem : 
A message containing letters A-Z is encoded using the mapping:

'A' -> "1"
'B' -> "2"
'C' -> "3"
....
'Z' -> "26"

Given a string s containg only digits , return the total number of ways to decode it

s = "12"
Output : 2

Explanation : 
"12" can be decoded as 
- "AB" (1 2)
- "L" (12)

Example 2:
s = "226"
Output : 
3

Explanation : 
"BZ" -> (2 26)
"VF" -> (22 6)
"BBF" -> (2 2 6)

💡 Intuition

You can think of this as:

“At every index, decide whether to decode one digit or two digits (if valid).”

If s[i] != '0',
then you can take one digit → dp[i] = dp[i-1]

If s[i-1..i] forms a valid number between 10 and 26,
then you can take two digits → dp[i] += dp[i-2]

                            class Solution {
                                public int numDecodings(String s) {
                                    int n = s.length();
                                    if (n == 0 || s.charAt(0) == '0') return 0;

                                    int[] dp = new int[n + 1];
                                    dp[0] = 1; // Empty string has one way to decode
                                    dp[1] = 1; // Non-zero single digit has one way

                                    for (int i = 2; i <= n; i++) {
                                        int oneDigit = s.charAt(i - 1) - '0';
                                        int twoDigits = Integer.parseInt(s.substring(i - 2, i));

                                        if (oneDigit >= 1)
                                            dp[i] += dp[i - 1]; // single digit decode
                                        if (twoDigits >= 10 && twoDigits <= 26)
                                            dp[i] += dp[i - 2]; // two digits decode
                                    }

                                    return dp[n];
                                }
                            }
