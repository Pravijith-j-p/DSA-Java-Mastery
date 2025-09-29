Problem Statement

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum, and return its sum.

Example:

🔹 Leetcode : 53

Input : nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output : 6
Explanation : [4, -1, 2, 1] has the largest sum = 6

🔹 Brute Force Approach

    -check all possible subarrays and calculate their sums.
    -track the maximum sum

            int maxSum = Integer.MIN_VALUE;
            for (int i =0; i< nums.length; i++){
                int currentSum = 0;
                for(int j = i; j< nums.length; j++){
                    currentSum += nums[j];
                    maxSum = Math.max(maxSum, currentSum);
                }
            }
            return maxSum;

    time complexity : O(n^2)
    space complexity: O(1)

🔹 Optimized Approach – Kadane’s Algorithm

    Maintain currentsum while iterating
    If currentsum becomes negative, reset it to 0(it can't contribute to maximum sum)
    track maximum sum so far

            public int maxSubArray ( int [] nums ){
                int maxSoFar = nums [0];
                int currentSum = nums [0];

                for (int i =1; i< nums.length; i++){
                    currentSum = Math.max(nums[i], currentSum + nums[i]);
                    maxSoFar = Math.max(MaxSoFar, currentSum);
                }

                return maxSoFar;
            }
    
    Timecomplexity : O(n) - single pass
    Spacecomplexity : O(1) - constant space


🔹 Step-by-Step Example

            nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

            initialize ;
            currentSum = maxSoFar = -2

            - Step 1: i=1, nums[1] = 1
            currentSum = max (1, -2+1) = 1
            maxSoFar = max (-2, 1 ) = 1

            - Step 2: i=2, nums [2] = -3
            currentSum = max (-3, 1-3) =-2
            maxSoFar = max(1, -2) = 1

            - Step 3: i=3, nums [3] = 4
            currentSum = max (4, -2+4) = 4
            maxSoFar = max(1, 4) = 4

            - Step 4: i=4, nums [4] = -1 
            currentSum = max (-1, 4+ -1) = 3
            maxSoFar = max(4, 3) = 4

            - Step 5: i=5, nums[5]=2
            currentSum = max(2, 3+2) = 5
            maxSoFar = max(4,5) = 5

            - Step 6: i=6, nums[6]=1
            currentSum = max(1,5+1) = 6
            maxSoFar = max(5,6) = 6

            - Step 7: i=7, nums[7]=-5
            currentSum = max(-5,6-5) = 1
            maxSoFar = max(6,1) = 6

            - Step 8: i=8, nums[8]=4
            currentSum = max(4,1+4) = 5
            maxSoFar = max(6,5) = 6

            Result = 6

Extensions of Kadane's Pattern

1. Maximum Product Subarray -> LEETCODE 152

                public int maxProduct (int [] nums ){
                    int maxProd = nums[0], minProd = nums[0], result = nums[0];
                    for(int i = 1;i< nums.length; i++){
                        int temp =maxProd;
                        maxProd = Math.max(nums[i], Math.max(maxProd * nums[i], minProd * nums[i]));
                        minProd = Math.min(nums[i], Math.min(temp * nums[i], minProd * nums[i]));
                        result = Math.max (result, maxProd);
                    }
                    return result;
                }

    - Time : O(n)
      Space : O(1)

    Example :
     
     Input nums = [2, 3, -2, 4]
     Output : 6
     Explanation : [2,3] has the largest product = 6

🔹 Key Idea

- unlike sum (Kadane's), product can flip signs.
- A large negative product can become a large positive if multiplied by another negative.
- So we need to track:
    maxProd -> maximum product ending at current index
    minProd -> minimum product ending at current index (important for sign flip)

    maxProd = max(nums[i], maxProd * nums[i], minProd * nums[i])
    minProd = min(nums[i], maxProd * nums[i], minProd * nums[i])


Step 1: Initialize

    nums = [2, 3, -2, 4]

    maxProd = 2
    minProd = 2
    result = 2

Step 2: i = 1(num = 3)

    tempMax = max(3, 2*3, 2*3) = 6
    tempMin = min(3, 2*3, 2*3) = 3

    maxProd = 6
    minProd = 3
    result = max(2,6) = 6

 Step 3: i = 2(num = -2)

    tempMax = max (-2, 6*-2, 3 * -2) = max(-2, -12, -6) = -2
    temMin  = min(-2, 6*-2, 3 *  -2) = min(-2, -12, -6) = -12
    result = max (6, 2) = 6

    
