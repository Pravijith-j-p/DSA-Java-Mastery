Leetcode 42

Problem : Given a string s consisting of uppercase English letters and an integer k, you can replace at most k characters with any uppercase letter.Find the length of the longest substring containing the same letter after at most k replacements

Input : s = "AABABBA", k = 1
Output : 4
Explanation : Replace the one 'A' in the middle to get "AABBBBA" or "AAAA**B**BA".
Longest substring with same letters = 4

🔹 Brute force approach

Idea : 
- Generate all substrings
-  for each substring, count the max frequency of a character
- if substring length minus max frequency <= k ->valid substring
- track the maximum length of all valid substrings

Time complexity : O(n^3)

                        public int characterReplacementBruteForce(String s, int k){
                            int n = s,length();
                            int maxLen = 0;

                            for(int i=0;i<n;i++){
                                for(int j=1;j<n;j++){
                                    int [] count = new int [26];
                                    for(int t = i;t <= j;t++){
                                        count [s.charAt(t) - 'A'] ++;
                                    }
                                    int maxFreq = 0;
                                    for(int c :count) maxFreq = Math.max(maxFreq, c);
                                    if(j - i + 1 - maxFreq <= k){
                                        maxLen = Math.max(maxLen, j - i + 1);
                                    }
                                }
                            }
                            return maxLen;
                        }

🔹 Optimized Approach (Sliding window)

- Maintain a sliding window [left, right]
- track MaxFreq = frequency of most common character in the window
- If (window size - maxFreq) > k, shrink window from left.
- The window always represents a valid substring after at most k replacements

public int characterReplacement(String s, int k){
    int [] count = new int [26];
    int maxFreq = 0;
    int left = 0; maxLen = 0;

    for(int right = 0; right < s.length(); right++){
        count[s.charAt(right) - 'A']++;
        maxFreq = Math.max(maxFreq, count[s.charAt(right) - 'A']);

        while((right - left + 1) - maxFreq > k){
            count[s.charAt(left) - 'A']--;
            left ++;
        }
        maxLen = Math.max(maxLen,  right - left +1);
    }
    return maxLen;
}

Time complexity  : O(n)
Space complexity  : O(1)

s = "AABABBA", k = 1

Step-by-step Dry Run

We keep:

left pointer

right pointer (expands window)

count[26] frequency array

maxFreq → frequency of most common character in window

(window size - maxFreq) → number of replacements needed

Initial state:

left = 0, right = 0, maxFreq = 0, maxLen = 0

Iteration:

1. right = 0 → "A"

Count = {A:1}

maxFreq = 1

Window size = 1 → valid (1 - 1 = 0 ≤ 1)

maxLen = 1

2. right = 1 → "AA"

Count = {A:2}

maxFreq = 2

Window size = 2 → valid (2 - 2 = 0 ≤ 1)

maxLen = 2

3. right = 2 → "AAB"

Count = {A:2, B:1}

maxFreq = 2

Window size = 3 → valid (3 - 2 = 1 ≤ 1)

maxLen = 3

4. right = 3 → "AABA"

Count = {A:3, B:1}

maxFreq = 3

Window size = 4 → valid (4 - 3 = 1 ≤ 1)

maxLen = 4

5. right = 4 → "AABAB"

Count = {A:3, B:2}

maxFreq = 3

Window size = 5 → invalid (5 - 3 = 2 > 1)

Shrink window: move left → 1

Remove s[0] = "A" → Count = {A:2, B:2}

Window size = 4 (valid now)

maxLen = 4

6. right = 5 → "ABABB"

Count = {A:2, B:3}

maxFreq = 3

Window size = 5 → valid (5 - 3 = 2 > 1)

Shrink: move left = 2

Remove s[1] = "A" → Count = {A:1, B:3}

Window size = 4 → valid

maxLen = 4

7. right = 6 → "BABBA"

Count = {A:2, B:3}

maxFreq = 3

Window size = 5 → valid (5 - 3 = 2 > 1)

Shrink: move left = 3

Remove s[2] = "B" → Count = {A:2, B:2}

Window size = 4 → valid

maxLen = 4