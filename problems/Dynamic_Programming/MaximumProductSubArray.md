Leetcode 152

Problem :
Given an integer array nums ,find the contigous subarray (containing at least one number) which has the largest product, and return that product

Example :
Input :
nums = [2, 3, -2, 4]

Output : 
6

Explanation : The subarray [2, 3] has the largest product  = 6

Example 2:
Input : nums = [-2, 0, 1]
Output : 
0

Explanation : The result cannot be true, because array must be contigous

Intution : 
Unlike maximum sum problems, product problems are tricky because:
- Multiplying by a negative number flips the sign
- Multiplying by zero resets the product

So, at each index i, the maximum product can become minimum if nums[i] is negative — and vice versa.

🧠 Dynamic Programming Idea

Let:

maxProd[i] = maximum product subarray ending at index i

minProd[i] = minimum product subarray ending at index i

Because:

If nums[i] is positive, it helps to continue max.

If nums[i] is negative, the previous min could become the new max.

                    class Solution {
                        public int maxProduct(int[] nums) {
                            int n = nums.length;
                            int maxProd = nums[0];
                            int minProd = nums[0];
                            int result = nums[0];

                            for (int i = 1; i < n; i++) {
                                int curr = nums[i];

                                // When multiplied by a negative number, swap min and max
                                if (curr < 0) {
                                    int temp = maxProd;
                                    maxProd = minProd;
                                    minProd = temp;
                                }

                                maxProd = Math.max(curr, curr * maxProd);
                                minProd = Math.min(curr, curr * minProd);

                                result = Math.max(result, maxProd);
                            }

                            return result;
                        }
                    }

🔍 Example Walkthrough

| i | num | maxProd | minProd | result | Explanation          |
| - | --- | ------- | ------- | ------ | -------------------- |
| 0 | 2   | 2       | 2       | 2      | start                |
| 1 | 3   | 6       | 3       | 6      | 2×3=6                |
| 2 | -2  | -2      | -12     | 6      | negative flips roles |
| 3 | 4   | 4       | -48     | 6      | only 4 > -2×4        |
