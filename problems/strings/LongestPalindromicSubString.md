Leetcode 5

Pattern/Key Idea : Expand around center/Dynamic Programming

Problem statement : Given a string s, find the longest substring that is palindrome

- A palindrome reads the same forwards and backwards

Example: 
Input : s = "babad"
Output: "bab" or "aba"

Input : s = "cbbd"
Output : "bb"

🔹 Approach 1 :Brute Force

Check all substrings and see if they are palindrome.
Keep track of the longest

                            public String longestPalindrome(String s){
                                if( s == null || s.length == 0) return "";

                                int maxLen = 0;
                                String longest = "";

                                for(int i = 0;i< s.length; i++){
                                    for(int j = 0;j< s.length; j++){
                                        String sub = s.substring(i, j + 1);
                                        if(isPalindrome(sub) && sub.length() > maxLen){
                                            maxLen = sub.length();
                                            longest = sub;
                                        }
                                    }
                                }
                                return longest;
                            }

                            private boolean isPalindrome(String s){
                                int left = 0; right = s.length - 1;
                                while(left < right){
                                    if(s.charAt(left) != s.charAt(right)) return false;
                                    left ++;
                                    right --;
                                }
                                return true;
                            }
Time complexity : O(n^3)
Space complexity : O(1)

🔹 Optimal solution : Expand around center(Optimal)
- Every palindrome is centered at a character or between two characters.
- Expand left and right from the center until mismatch

                                public String longestPalindrom (String s) {
                                    if(s == null || s.length() < 1) return "";
                                    int start = 0, end =0;
                                    for(int  i = 0; i <s.length(); i++){
                                        int len 1 = expandFromCenter(s, i, i);  //odd length
                                        int len 2 = expandFromCenter(s, i, i+1); //even length
                                        int len = Math.max(len1, len2);
                                        if(len > end - start) {
                                            start = i-(len-1)/2;
                                            end = i+len/2;
                                        }
                                    }
                                    return s.substring(start, end+1);
                                }

                                private int expandFromCenter(String s,int left, int right){
                                    while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)){
                                        left --;
                                        right ++;
                                    }
                                    return right - left - 1;
                                }
Time complexity : O(n^2)
Space complexity : O(1)
