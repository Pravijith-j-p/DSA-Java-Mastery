Leetcode 139

Problem : 
Given a string s and a dictionary if strings wordDict,
return true if s can be segmeneted into a space-separated sequence of one or more dictionary words

Example : 
Input : 
s = "leetcode"
wordDict = ["leet", "code"]

Output : true;

Explanation : "leetcode" -> "leet" + "code"

Example 2:
s = "applepenapple"
wordDict = ["apple", "pen"]

Output : 
true

Explanation : 
"apple" + "pen" + "apple"

💡 Intuition

We check whether we can **split the string into valid dictionary words**.  

Let’s define:

⚡ Optimization Tips

To speed up substring lookups → use a Trie or store words in a HashSet (as we did).

Avoid repeated substring() creation by caching dictionary words by length.

                            class Solution {
                                public boolean wordBreak(String s, List<String> wordDict) {
                                    return helper(s, new HashSet<>(wordDict), 0, new Boolean[s.length()]);
                                }

                                private boolean helper(String s, Set<String> dict, int start, Boolean[] memo) {
                                    if (start == s.length()) return true;
                                    if (memo[start] != null) return memo[start];

                                    for (int end = start + 1; end <= s.length(); end++) {
                                        if (dict.contains(s.substring(start, end)) && helper(s, dict, end, memo)) {
                                            return memo[start] = true;
                                        }
                                    }

                                    return memo[start] = false;
                                }
                            }

Memoization (Top-Down DP)
Time  : O(n²)
Space : O(n)

