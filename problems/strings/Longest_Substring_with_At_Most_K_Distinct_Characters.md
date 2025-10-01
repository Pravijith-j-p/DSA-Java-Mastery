Leetcode 340

Problem statement 
Given a string s and an integer k, return the length of the longest substring that contains atmost k distinct characters.

Examples

example 1 : 
Input : s = "eceba", k = 2
Output : 3
Explanation : "ece" is the longest substring with atmost 2 characters

Input: s = "aa", k = 1
Output : 2
Explanation : "aa" is the longest substring with only 1 distinct character.

🔹 Brute Force Approach

Generate all substrings.
For each substring, check if ithas atmost k distinct characters.
Track the maximum length

Time Complexity : O(n^3)
Space complexity : O(n) (to store substring sets).

                    public int lengthOfLongestSubstringKDistinctBrutforce(String s, int k){
                        int n = s.length(), maxLen = 0;
                        for(int i = 0;i<n ; i++){
                            Set<Character> set = new HashSet <>();
                            for(int j=i; j< n; j++){
                                set.add(s.charAt())
                                if(set.size() <= k){
                                    maxLen = Math.max(maxLen, j - i +1);
                                }else break;
                            }
                            
                        }
                        return maxLen;
                    }

🔹 Optimized Approach: Sliding Window + HashMap

Idea : We expand the window with the right pointer, and maintain the count of each character in a HashMap.
if distinct characters exceed k , shrink from the left until we are back to atmost k distinct characters.

Algorithm:

1. Use HashMap<Character, Integer> to store character counts
2. Expand right pointer, adding characters into the map.
3. If map.size() > k, shrink from left by decreasing counts.Remove char if count = 0.
4. Track max window length

Time complexity : O(n) (each charcter processed atmost twice)
Space complexity : O(k)

                        public class LongestSubstringKDistinct(String s , int k){
                            Map<Character, Integer> map = new HashMap <>();
                            int left =0; maxLen = 0;

                            for(int right = 0; right<s.length(); right++){
                                char c = s.charAt(right);
                                map.put(c, map.getOrDefault(c, 0) + 1);

                                while(map.size() > k){
                                    char leftChar = s.charAt(left);
                                    map.put(leftChar, map.get(leftChar) - 1);
                                    if(map.get(leftchar) == 0){
                                        map.remove(leftChar);
                                    }
                                    left ++;
                                }
                                maxLen = Math.max(maxLen, right - left + 1);
                            }
                            return maxLen;
                        }

Step-by-Step Dry Run

Input : s = "eceba" , k=2

| Step | left | right | char | map                                | maxLen |
| ---- | ---- | ----- | ---- | ---------------------------------- | ------ |
| 1    | 0    | 0     | e    | {e=1}                              | 1      |
| 2    | 0    | 1     | c    | {e=1, c=1}                         | 2      |
| 3    | 0    | 2     | e    | {e=2, c=1}                         | 3      |
| 4    | 0    | 3     | b    | {e=2, c=1, b=1}                    | 3      |
|      | 1→2  |       |      | shrink → {e=1,c=1,b=1} → {e=1,b=1} |        |
| 5    | 2    | 4     | a    | {e=1, b=1, a=1}                    | 3      |
|      | 2→3  |       |      | shrink → {b=1,a=1}                 |        |

