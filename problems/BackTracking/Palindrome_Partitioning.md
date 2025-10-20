Leetcode 131

Problem :
Given a string , partition s such that every substring in the partition is a palindrome
Return all possible palindrome partitioning of s

Example : 
Input :
 s = "aab"

 Output : 
 [
    ["a", "a", "b"],
    ["aa", "b"]
 ]

 Key Idea - Backtracking

We explore all possible places to "cut" the string and check if the left substring is a palindrome:
    - If yes -> recursively partition the remaining right substring
    - if we reach the end -> that's one partition
So it's DFS on substring splits + palindrome check

⚙️ Approach 
1. Start from index 0
2. Try every possible end index from start to n-1.
3. If s[start...end] is palindrome
    - add it to the current partition list
    - Recurse for the remaining substring starting from end + 1.
4. When start == s.length(),add the current list to the result


                                class Solution {
                                    public List<List<String>> partition(String s) {
                                        List<List<String>> result = new ArrayList<>();
                                        backtrack(result, new ArrayList<>(), s, 0);
                                        return result;
                                    }

                                    private void backtrack(List<List<String>> result, List<String> current, String s, int start) {
                                        if (start == s.length()) {
                                            result.add(new ArrayList<>(current));
                                            return;
                                        }

                                        for (int end = start; end < s.length(); end++) {
                                            if (isPalindrome(s, start, end)) {
                                                current.add(s.substring(start, end + 1));  // Choose
                                                backtrack(result, current, s, end + 1);    // Explore
                                                current.remove(current.size() - 1);        // Un-choose
                                            }
                                        }
                                    }

                                    private boolean isPalindrome(String s, int left, int right) {
                                        while (left < right) {
                                            if (s.charAt(left++) != s.charAt(right--))
                                                return false;
                                        }
                                        return true;
                                    }

                                    public static void main(String[] args) {
                                        Solution sol = new Solution();
                                        List<List<String>> res = sol.partition("aab");
                                        for (List<String> part : res) {
                                            System.out.println(part);
                                        }
                                    }
                                }
🧮 Complexity Analysis
| Type                 | Complexity                                                                              |
| -------------------- | --------------------------------------------------------------------------------------- |
| **Time Complexity**  | O(N × 2ⁿ) — there are 2ⁿ ways to partition a string, and palindrome checking takes O(N) |
| **Space Complexity** | O(N) recursion depth + result storage                                                   |

🧠 Example Dry Run ("aab")

| Step | Current Partition    | Next Start                | Explanation                |
| ---- | -------------------- | ------------------------- | -------------------------- |
| 1    | `["a"]`              | 1                         | "a" is palindrome          |
| 2    | `["a","a"]`          | 2                         | second "a" also palindrome |
| 3    | `["a","a","b"]`      | 3 (end)                   | valid → add result         |
| 4    | backtrack to `["a"]` | try "ab" → not palindrome |                            |
| 5    | backtrack to `[]`    | try "aa" (palindrome)     |                            |
| 6    | `["aa","b"]` → valid |                           |                            |

