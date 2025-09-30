Leetcode 325

Problem statement

Given an array of integers nums and an integer k , find the maximum sum of any contiguous subarray of size k

Example 
    Input : [2, 1, 5, 1, 3, 2], k = 3
    Output : 9
    Explanation : Subarray [5, 1, 3] has the maximum sum = 9.

    Input : [2, 3, 4, 1, 5], k=2
    Output : 7
    Explanation : Subarray [3, 4] has the maximum sum = 7

🔹 Brute Force Approach

- check sum of all subarray of size k using nested loops:

                public int maxSubBrute (int [] nums , int k){
                    int n = nums.length;
                    int maxSum = Integer.MIN_VALUE;
                    for(int i = 0; i<= n-k; i++){
                        int sum = 0;
                        for(int j = i; j< i + k; j++){
                            sum += nums [j];
                        }
                        maxSum = Math.max(maxSum, sum);
                    }
                    return maxSum;
                }

Time : O(n * k)
Space : O(1)

🔹 Optimized Approach: Sliding Window

(📌 Definition

A sliding window is a contiguous subset of elements in an array or string that “slides” over the data structure to examine a portion at a time, instead of checking everything from scratch.)

- maintain current sum of window size k
- slide the window by adding the next element and the first element of previous window

            public int maxSumSlidingWindow(int [] nums, int k){
                int n =nums.length;
                int windowSum = 0;

                //intial window
                for(int i = 0; i < k; i++){
                    windowSum += nums[i];
                }

                int maxSum = windowSum;

                //slide the window
                for(int i = k; i< n; i++){
                    windowSum += nums[i] - nums [i - k];            //add next remove first
                    maxSum = Math.max(maxSum, windowSum);
                }
                return maxSum;
            }
Time : O(n)
Space : O(1)

Example : 

nums = [2, 1, 5, 1, 3, 2], k = 3
Goal : Find maximum sum of any contigous subarray of size 3

Step 1 : Initialize

- windowSum = sum of first k elements = 2+ 1+ 5 = 8
- maxSum = 8
- Window: [2, 1, 5]

Step 2 : Slide the window

- Move window one step to the right
- Remove nums [0] = 2, add nums [3] = 1
  windowSum = 8 -2 + 1 = 7
- update maxSum = max(8, 7) = 8
- window : [5, 1 , 3]

Step 3 : Slide again 
- remove nums[1] = 1 and add nums [4] = 3
- windowSum = 7 - 1 + 3 = 9
- update maxSum = max(8, 9) = 9 
- window : [5, 1, 3] 

Step 4 : Slide one more
- Remove nums [2] = 5 and add nums[5] = 2
- windowSum = 9 - 5 + 2 = 6
- update maxSum = max(9, 6) = 9
- window : [1, 3, 2]

Step 5 : End
No more window of size k
Result = 9

