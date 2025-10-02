Leetcode 76

Problem : Given two strings s and t, return the minimum window substring of s that contains all the characters of t.If there is no such substring, return an empty string.

Example 1 :
Input : s ="ADOBECODEBANC" , t = "ABC"
Output : "BANC"

Explanation : "BANC is the smallest substring of s that contains 'A','B','C'.

Example 2 : 
Input : s = "a", t = "aa"
Output: ""
Explanation : t cannot be formed from s

🔹 Brute Force Approach

- Generate all substrings of s
- For each substring, check if it contains all characters of t
- Track the smallest valid substring

Time Complexity : O(n^2)


                    public String minWindow(String s, String t){
                        if(s.length() < t.length()) return "";

                        int minLen = Integer.MAX_VALUE;
                        String result = "";

                        for(int i = 0; i< s.length(); i++){
                            for(int j = i+1; j<= s.length(); j++){
                                String sub = s.substring(i , j);

                                if(containsAll(sub, t)){
                                    if(sub.length() < minLen){
                                        minLen = sub.length();
                                        result = sub;
                                    }
                                }
                            }
                        }
                        return result;
                    }

                    private boolean containsAll(String sub, String t){
                        Map<Character, Integer> count = new HashMap<>();
                        for(char c :sub.toCharArray()){
                            count.put(c, count.getOrDefault(c, 0) + 1);
                        }
                        for(char c :t.sub.toCharArrat()){
                            if(!count.containsKey(c) || count.get(c) == 0) return false;
                            count.put(c, count.get(c) - 1);
                        }
                        return true;
                    }

🔹 Optimized Sliding Window + HashMap Approach

Idea : 
- use two HashMaps (or arrays for 26/128 chars):
    - need: frequency count of charcters in t
    - have : frequency count of current window in s
- expand right pointer and include characters
- when all pointers from t are satisfied in the current window-> try to shrink with left to minimize window size
- Keep track of smallest valid window

                    public String(String s, String t){
                        if(s.length() < t.length()) return "";

                        Map<Character, Integer> map = new HashMap<>();
                        for(char c :t.toCharArray()){
                            need.put(c, need.getOrDefault(c, 0) + 1);
                        }
                        int left = 0, right = 0;
                        int required = need.size();
                        int formed = 0;

                        Map<Charcter ,Integer> window = new HashMap<>();
                        int minLen = Integer.MAX_VALUE;
                        int start = 0;

                        while (right < s.length()){
                            char c = s.charAt(right);
                            window.put(c, window.getOrDefault(c, 0) + 1);

                            if(need.containsKey(c) && window.get(c).intValue() == need.get(c).intValue()){
                                formed++;
                            }
                            while(left <= right && formed == required) {
                                if(right - left + 1 < minLen) {
                                    minLen = right - left + 1;
                                    start = left;
                                }
                                char leftChar = s.charAt(left);
                                window.put(leftChar, window.get(leftChar) - 1);
                                if(need.containsKey(leftChar) && window.get(leftChar) < need.get(leftChar)){
                                    formed --;
                                }
                                left ++;
                            }
                            right ++;
                        }
                        return minLen = Integer.MAX_VALUE ? "" : s.substring(start, start + minLen);
                    }
                    
Dry Run (s = "ADOBECODEBANC", t = "ABC")

need = {A:1, B:1, C:1}

Expand window until it contains "ABC" → "ADOBEC"

Shrink from left until minimal valid → "BEC"

Expand again to "BANC" → minimal valid window updated → "BANC" ✅