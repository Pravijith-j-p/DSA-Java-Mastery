Leetcode 763

Problem Summary

You are given a string s. You must partition it into as many parts as possible so that each letter appears in at most one part.
Return a list containing the size of each partition.

✅ Intuition

We want to cut the string into segments where all occurrences of each character stay in the same segment.

To do this:

First record the last occurrence index of every character.

Use two pointers:

start = beginning of the current partition

end = furthest last occurrence seen so far

Traverse the string:

Update end = max(end, lastIndex[s[i]])

When i == end, we finish a partition → save length and move start = i+1.

This works because once i reaches the maximum last occurrence of all characters seen until now, the block is self-contained.

Example
s = "ababcbacadefegdehijhklij"
Output = [9, 7, 8]


Because:

"ababcbaca" → all chars end by index 8

"defegde" → ends at index 15

"hijhklij" → ends at index 23

class Solution {
    public List<Integer> partitionLabels(String s) {
        int[] last = new int[26];

        // Store last occurrence of each character
        for (int i = 0; i < s.length(); i++) {
            last[s.charAt(i) - 'a'] = i;
        }

        List<Integer> result = new ArrayList<>();
        int start = 0, end = 0;

        // Create partitions
        for (int i = 0; i < s.length(); i++) {
            end = Math.max(end, last[s.charAt(i) - 'a']);
            if (i == end) {
                result.add(end - start + 1);
                start = i + 1;
            }
        }

        return result;
    }
}
