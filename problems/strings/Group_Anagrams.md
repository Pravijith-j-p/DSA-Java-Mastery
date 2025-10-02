Leetcode 49 

Pattern/Key Idea : HashMap/Frequency Count or Sorted string as a key

Problem : Given an array of strings strs, group the anagrams together

- You can return the answer in any order

Example: 
Input : strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
Output : [["eat", "tea", "ate"],["tan", "nat"], ["bat"]]

🔹 Approach 1: Brute Force (Sorting strings)
- Sort each string and use sorted string as Key in HashMap
- Group all original strings with the same sorted key

                    class Solution{
                        public List<List<String>> groupAnagrams(String [] strs){
                            if(strs == null || strs.length == 0) return new ArrayList<>();
                            Map<String, List<String>> map = new HashMap<>();

                            for(String s: strs){
                                char[] chars =s.toCharArray();
                                Arrays.sort(chars);
                                String key = new String(chars);

                                if(!map.containsKey(key)) map.pu(key, new ArrayList<>());
                                map.get(key).add(s);
                            }
                            return new ArrayList<>(map.values());
                        }
                    }
Time complexity : O(n*klogn) 
Space complexity : O(n*k)

🔹 Optimized Approach :
- Instead of sorting , use frequency of characters as a Key
- Create a string key like "a2b1c0.." representing counts of each character

                        class Solution{
                            public List<List<String>> groupAnagrams(String[] strs){
                                if(strs == null|| strs.length ==0) return new ArrayList<>();
                                Map<String, List<String>> map = new HashMap<>();

                                for(String s :strs){
                                    int [] count = new int[26];
                                    for(char c : s.toCharArray()) count[c - 'a']++;

                                    StringBuilder sb = new StringBuilder();
                                    for(int i : count) sb.append(i).append('#'); //delimiter
                                    String key = sb.toString();

                                    if(!map.containsKey(key)) map.put(key, new ArrayList<>());
                                    map.get(key).add(s);
                                }
                                return new ArrayList<>(map.values());
                            }
                        }
Time complexity : O(n*k)
Space complexity : O(n*k)

