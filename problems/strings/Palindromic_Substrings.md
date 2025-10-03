Leetcode : 647

Problem : Given a string s, return the number of palindromic substrings in it

A substring is palindromic if it reads the same backward and forward

Example 1:
Input : s = "abc"
Output : 3

Explanation:
- each character is a palindrome -> "a","b","c"

Example 2:
Input : s = "aaa"
Output : 6
Explanation: Palindromic substrings are "a","a","a","aa","aa","aaa"

🔹 Brute Force Approach (Check all substrings)

                        public int countSubstring(String s){
                            int n = s.length;
                            int count = 0;
                            for(int i = 0;i<n; i++){
                                for(int j=i;j<n ;j++){
                                    if(Palindrome(s, i, j)){
                                        count ++;
                                    }
                                }
                            }
                            return count;
                        }

                        private boolean isPalindrome(String s, int l, int r){
                            while (l < r){
                                if (s.charAt(l++) != s.charAt(r--)) return false;
                            }
                            return true;
                        }
Time complexity : O(n^2)
Space complexity : O(1)

🔹 Optimized Approach (Expand Around Center) ✅

                        public int countSubstring(String s){
                            int n =s.length();
                            int count  = 0;

                            for(int center = 0; center < 2*n -1;center++){
                                int left = center /2;
                                int right = left + center % 2;

                                while (left >= 0 && right < n && s.charAt(left) == s.charAt(right)){
                                    count ++;
                                    left --;
                                    right ++;
                                }
                            }
                            return count;
                        }

Key Idea:
- A palindrome expands from its center
- Each center can be:
  - a single character (odd length palindrome)
  - between two characters(even length palindrome)
-Total centers = 2n - 1

Time complexity : O(n^2)
Space complexity : O(1)