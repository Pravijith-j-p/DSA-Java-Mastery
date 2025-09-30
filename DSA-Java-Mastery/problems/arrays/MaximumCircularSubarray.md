Problem Statement

Leetcode 918 :

Given a circular integer array nums, find the contiguous subarray with the largest sum.

 (Circular array means the end of the array wraps around to the beginning)

 Example 1 :
        Input = nums = [1, -2, 3, -2]
        Output : 3
        Explanation : Subarray [3] has the maximum sum = 3

 Example 2 :
        Input: nums = [5, -3, 5]
        Output: 10 
        Explanation : Subarray [5, 5] (wrap around) has the maximum sum = 10


🔹 Key Idea

-> Maximum sum in a circular array can be either :
    1. Normal max subarray -> no wrap around -> using Kadane's algorithm
    2. Wrap around subarray -> sum of total array minus minimum subarray sum

Formula : 
        maxSumCircular = max(Kadane(nums), totalSum - Kadane(-nums))

        Optimized Approach (Kadane + Total Sum)

        public int maxSubarraySumCircular (int [] nums){
            int total = 0;
            int maxSum = nums [0], curMax = 0;
            int minSum = nums [0], curMin = 0;

            for(int num: nums){
                curMax = Math.max(num, curMax + num);
                maxSum = Math.max(maxSum, curMax);

                curMin = Math.min(num, curMin + num);
                minSum = Math.min(minSum, curMin);

                total += num;
            }
            //edge case : all negative numbers
            return maxSum > 0 ? Math.max(maxSum, total - minSum) : maxSum;
        }

Time complexity : O(n) - single pass
Space complexity : 0(1) - constant space

Example:
  nums=[5, -3, 5]

    | Index | num | curMax (Kadane)     | maxSum        | curMin (Min Subarray) | minSum          | total        |
    | ----- | --- | ------------------- | ------------- | --------------------- | --------------- | ------------ |
    | 0     | 5   | 5                   | 5             | 5                     | 5               | 5            |
    | 1     | -3  | max(-3, 5+(-3)) = 2 | max(5, 2) = 5 | min(-3, 5+(-3)) = -3  | min(5, -3) = -3 | 5 + (-3) = 2 |
    | 2     | 5   | max(5, 2+5) = 7     | max(5, 7) = 7 | min(5, -3+5) = 2      | min(-3, 2) = -3 | 2 + 5 = 7    |
