Leetcode 300

Problem:

Given an integer array nums, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from the array by deleting some or no elements without changing the order of the remaining elements

Example : 
Input : 
nums = [10, 9, 2, 5, 3, 7, 101, 18]

Output : 4

Explanation : The longest increasing subsequence is [2, 3, 7, 101], so the length is 4

Example 2:
nums = [0,1,0,3,2,3]```  
**Output:** `4`  
**Explanation:** LIS = `[0,1,2,3]`

Optimized approach - Binary search

        class Solution {
            public int lengthOfLIS(int[] nums) {
                List<Integer> lis = new ArrayList<>();

        for (int num : nums) {
            int pos = Collections.binarySearch(lis, num);
            if (pos < 0) pos = -(pos + 1); // get insertion index
            if (pos == lis.size()) lis.add(num);
            else lis.set(pos, num);
        }

        return lis.size();
    }
    }
