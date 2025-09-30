Problem Statement

Given an integer array nums, return an array answer such that

answer [i] = prodct of all elements of nums except nums[i]

Constrains : 

Solve without using division
Time Complexity O(n), space complexity O(1) (excluding output array)

Example 1: 

    input : nums =[1, 2, 3, 4]
    output : [24, 12, 8, 6]
    Explanation :
    - answer[0] = 2*3*4 =24
    - answer[1] = 1*3*4 =12
    - answer[2] = 1*2*4 =8
    - answer[3] = 1*2*3 =6

Example 2 :

    input : nums = [-1, 1, 0, -3, 3]
    output : [0, 0, 9, 0, 0]

🔹 Brute Force Approach

- multiply all other elements for each index
- Time: O(n^2), Space :O(1)

            for (int i=0; i <nums.length; i++){
                int prod = 1;
                for (int j=0; j<nums.length; j++){
                    if(i != j) prod *= nums [j];
                }
                answer [i] = prod;
            }

🔹 Optimized Approach (Prefix & Suffix Products)

Idea:
- Compute prefix products (product of elements to the left of i)
- Compute suffix products (product of elements to the right of i)
- Multiply prefix[i] * suffix[i] for final answer

            public int [] productExceptSelf (int [] nums){
                int n = nums.length
                int [] answer = new int[n]; 

                //Step 1; prefix products
                answer [0] =1 ;

                for(int i=1; i<n; i++){
                    answer [i] = answer [i-1] * nums[i - 1];
                } 

                //Step 2 : suffix products
                int suffix = 1;
                for(int i= n-1; i>=0; i--){
                    answer [i] *= suffix;
                    suffix *= nums[i];
                }
                return answer;
            }

Time complexity : O(n) -single pass for prefix + suffix
Space complexity : O(1) extra(excluding output array)


Step by Step example 

    Input 

    nums = [1, 2, 3, 4]

        | Index | nums[i] | Prefix product | Suffix product | answer[i] |
        | ----- | ------- | -------------- | -------------- | --------- |
        | 0     | 1       | 1              | 24             | 24        |
        | 1     | 2       | 1              | 12             | 12        |
        | 2     | 3       | 2              | 4              | 8         |
        | 3     | 4       | 6              | 1              | 6         |


🔹 Edge Cases

Array contains zeros → suffix/prefix handles it automatically

Array length = 1 → answer = [1]

Negative numbers → works as usual

1️⃣ Typical Interview Phrasing

Direct / Classic:

“Given an array nums, return a new array such that each element at index i is the product of all elements in the array except nums[i]. Can you do it without using division?”

Variant / Real-world Scenario:

“You are given sales numbers for a week. For each day, compute the total sales excluding that day. Optimize your solution for large datasets.”

Hints / Leading Questions Interviewers Might Give:

“Can you do it in O(n) time?”

“Can you reduce extra space usage?”

“What happens if the array contains zeros?”

2️⃣ What Interviewers Are Testing
Concept	Why It’s Tested
Pattern recognition	Do you recognize that prefix & suffix arrays solve the problem efficiently?
Optimization	Can you go from O(n²) brute force to O(n)?
Edge-case handling	Can you handle zeros, negatives, single-element arrays?
In-place / space optimization	Can you reduce extra space to O(1) by reusing the output array?
Communication	Can you explain your approach clearly and walk through an example?

3️⃣ How to Approach in an Interview

Step 1: Clarify the question

Are division operations allowed?

Can the array have zeros or negative numbers?

Expected time & space complexity?

Step 2: Discuss the brute force approach

Nested loops → O(n²) → show that it’s too slow

Step 3: Introduce prefix & suffix approach

Draw an example array on the board

Explain how prefix * suffix gives the answer

Step 4: Optimize space (optional)

Reuse output array for prefix products

Use a single variable to track suffix product

Step 5: Walk through edge cases

Zeros, negative numbers, array length 1

Step 6: Conclude with time & space complexity