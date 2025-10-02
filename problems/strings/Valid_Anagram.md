Leetcode 242

Pattern/Key Idea : HashMap/Frequency counting

Problem : Given two strings s and t, determine if t is an anagram of s.
- An anagram is a word formed by rearranging the letters of other word, using all original letters exactly once.

Example : 
Input : s = "anagram", t = "nagaram"
Output : true

Input : s ="rat", t = "car"
Output : false

🔹 Brute Force Approach :
 - sort both strings and check if they are equal

                        public boolean isAnagram(String s, String t){
                            if(s.length != t.length ) return false;
                            char [] sArr = s.toCharArray();
                            char [] tArr = t.toCharArray();
                            Arrays.sort(sArr);
                            Arrays.sort(tArr);
                            return Arrays.equals(sArr, tArr);
                        }
Time Complexity : O(nlogn) (sorting)
Space Complexity : O(n)

🔹 Optimized approach
- count frequency of each character in s using HashMap
- Decrease counts while traversing t
- if all counts are zero at the end, strings are anagrams

                public boolean isAnagram(String s, String t){
                    if(s.length != t.length) return false;

                    HashMap <Character, Integer> map = new HashMap<>();
                    for(char c : s.toCharArray){
                        map.put(c, map.getOrDefault(c, 0) + 1);
                    }
                    for(char c : t.toCharArrat){
                        if(!map.containsKey(c)) return false;
                        map.put(c, map.get(c) - 1);
                        if(map.get(C) == 0) map.remove(c);
                    }
                    return map.IsEmpty();
                }
Time complexity : O(n)
Space Complexity : O(1) (since alphabet size is fixed)

