Leetcode 567

Problem : Given two strings s1 and s2
Write a function to return true if s2 contains a permutation of s1

Otherwise , return false

A permutation of a string is just a rearrangement of characters.

Example 1
Input : s1 ="ab", s2 = "eidbaooo"
Output : true
Explanation : "ba" is a permutation of "ab" that appears in "eidbaooo"

Example 2:
Input s1 = "ab" s2 = "eidboaoo"
Output : false;

🔵 Brute Force approach

- Generate all substrings of s2 with length = s1.length() and check if any substring is a permutation of s1
- to check permutation-> just compare character counts (or sort both and compare)

                        public boolean checkInclusion(String s1, String s2){
                            int n =s1.length;
                            int m =s2.length;

                            if(n > m) return false;

                            //Sort s1 for comparison
                            char [] s1Arr = s1.toCharArray();
                            java.util.Arrays.sort(s1Arr);
                            String sortedS1 = new String(s1Arr);

                            //check all substring of s2 with length n
                            for(int i =0;i<n; i++){
                                String sub = s2.substring(i, i+n);

                                char[] subArr = sub.toCharArray();
                                java.util.Arrays.sort(subArr);
                                String sortedSub = new String(subArr);

                                if(sortedS1.equals(sortedSub)) return true;
                            }
                            return false;
                        }
Time complexity : O(m * nlogn)
Space Complexity : O(n)

✅ Optimal Solution -> Sliding window + frequency array

1. Count the frequency of charcters of s1
2. use a sliding of size s1.length() on s2
3. for each window , check if its frequency matches s1's frequency
4. if yes-> return true
5. if we finish checking all windows finding  a match -> return false;

                        public boolen checkInclusion(String s1, String s2){
                            if(s1.length() > s2.length) return false;

                            int [] s1Count = new int[26];
                            int [] s2Count = new int[26];

                            //Count frequency of s1 and first window in s2
                            for(int i = 0;i< s1.length(); i++){
                                s1Count[s1.charAt(i)-'a']++;
                                s2Count[s2.charAt(i)-'a']++;
                            }

                            //check all windows
                            for(int i = 0;i<s2.length() - s1.length();i++){
                                if(matches(s1Count, s2Count)) return true;

                                //Slide window : remove left char, add right char
                                s2Count[s2.charAt(i) - 'a']--;
                                s2Count[s2.charAt(i + s1.length()) -'a' ]++;
                            }

                            //Final window check
                            return matches (s1Count, s2Count);
                        }
                        private boolean matches(int [] s1Count, int[]s2Count){
                            for(int i =0;i< 26;i++){
                                if(s1Count[i] != s2Count[i]) return false;
                            }
                            return true;
                        }

Time complexity : O(26*n) ->O(n)
Space complxity : O(26) -> O(1)



