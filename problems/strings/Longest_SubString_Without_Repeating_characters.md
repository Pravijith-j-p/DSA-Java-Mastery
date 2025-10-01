Leetcode 3

Problem Statement

Given a string s, find the length of the longest substring without repeating characters

Example:
    Input : s = "abcabcbb"
    Output : 3
    Explanation : The answer is "abc", with the length of 3.

    Input : s = "bbbbb"
    Output : 1
    Explanation : The answer is "b", with the length of 1.

    Inpput : s = "pwwkew"
    Output : 3
    Explanation : The answer is "wke", with the length of 3.


🔹 Brute Force Approach

Check all possible substrings and keep track of the maximum length of substring with all unique characters.

Algorithm:

1. Generate all substrings of s.
2. For each substring, check if all characters are unique
3. Keep track of the maximum length.

Time complexity : O(n^3)
Space complexity :O(min(n, charset)) -> to store characters for uniqueness check.

                    public int lengthOfLongestSubstringBruteForce(String s){
                        int n = s.length();
                        int maxLen = 0;

                        for(int i=0; i< n ; i++){
                            for(int j = i + 1;j<= n; j++){
                                String sub = s.substring(i, j);
                                if(allUnique(sub)){
                                    maxLen = Math.max(maxLen, j - i);
                                }
                            }
                        }
                        return maxLen;
                    }

                    private boolean allUnique(String s){
                        Set<Character> set = new HashSet<> ();
                        for(char c: s.toCharArray()){
                            if(set.contains(c)) return false;
                            set.add(c);
                        }
                        return true;
                    }

🔹 Optimized Approach: Sliding Window + HashSet

Idea : Use two pointers (window) to keep track of current substring with unique characters.

Algorithm : 
1. Initialize a HashSet to store charcters in the current window.
2. Use two pointers left and right representing window boundaries
3. Expand right pointer and add character to set if not present
4. If character is repeated, remove s[left] from set and mpve left.
5. Update maxLen after each iteration.

Time Complexity : O(n) -> each character is visited at most twicw
Space Complexity : O(min(n, charset)) -> store characters in set


                        public in lengthofLongestSubstring(String s){
                            Set<Character> set = new HashSet<> ();
                            int left = 0; maxLen = 0;

                            for(int right = 0; right < s.length(); right++){
                                char c = s.charAt(right);
                                while(set.contains(c)){
                                    set.remove(s.charAt(left));
                                    left ++;
                                }
                                set.add(c);
                                maxLen = Math.max(maxLen, right-left+1);
                            }
                            return maxLen;
                        }

Step-by-Step Dry Run
 Input : s = "abcabcbb"

| Step | left | right | char | set     | maxLen |
| ---- | ---- | ----- | ---- | ------- | ------ |
| 1    | 0    | 0     | a    | {a}     | 1      |
| 2    | 0    | 1     | b    | {a,b}   | 2      |
| 3    | 0    | 2     | c    | {a,b,c} | 3      |
| 4    | 0→1  | 3     | a    | {b,c,a} | 3      |
| 5    | 1→2  | 4     | b    | {c,a,b} | 3      |
| …    | …    | …     | …    | …       | …      |

Output : 3


Pattern / Reusable Concepts

Sliding Window → Maintain a window of unique elements.

Can be extended to:

- Longest substring with at most K distinct characters

- Minimum window substring containing all characters

- Longest substring with at most two distinct characters
