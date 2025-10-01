LeetCode 125

Problem statement 

Given an string s, determine if it's a palindrome, considering only alphanumeric characters and ingnoring cases.

Example 1:

Input : s = "A man, a plan, a canal: Panama"
Output : true
Explanation : After removing non-alphanumeric characters and converting to lowercase, s ="amanaplanacanalpanama", which is a palindrome

Example 2:
Input : s = "race a car"
Output : false
Explanation : After removing non-alphanumeric characters, s = "raceacar", which is not palindrome

🔹 Brute Force Approach

1. Remove all alphanumeric characters.
2. Convert the string to lowercase
3. Compare the string with its reverse

Time Complexity : O(n)
Space complexity : O(n) 

                    public boolean isPalindromeBrute(String s){
                        StringBuilder sb = new StringBuilder ();
                        for(char c: s.toCharArray()){
                            if(Character.isLetterOrDigit(c)){
                                sb.append(Character.toLowerCase(c));
                            }
                        }
                        String cleaned = sb.toString();
                        String reversed = sb.reverse().toString();
                        return cleaned.equals(reversed);
                    }

🔹 Optimized Approach: Two Pointers

1. Use two pointers left and right starting from both ends of the string
2. Skip non alphanumeric characters
3. Compare characters at left and right
4. If mismatch -> not palindrome
5. Move pointers inward until they cross.

Time complexity : O(n)
Space complexity : O(1)

                    public boolean isPalindrome(String s){
                        int left = 0, right = s.length - 1;

                        while(left < right){
                            while (left < right && !Character.isLetterOrDigits(s.charAt(left))) left ++;
                            while (left < right && !Charcter.isLetterOrDigits(s.charAt(right))) right--;

                            if(Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))){
                                return false;
                            }
                            left++;
                            right--;
                        }
                        return true;
                    }

Step-by-Step Dry Run

Input: "A man, a plan, a canal: Panama"

| Step | left | right | chars compared | move pointers   | result |
| ---- | ---- | ----- | -------------- | --------------- | ------ |
| 1    | 0    | 29    | 'A' vs 'a'     | left++, right-- | match  |
| 2    | 1    | 28    | ' ' vs 'm'     | skip space      | match  |
| 3    | 2    | 28    | 'm' vs 'm'     | left++, right-- | match  |
| …    | …    | …     | …              | …               | …      |

All matches -> Palindrome

