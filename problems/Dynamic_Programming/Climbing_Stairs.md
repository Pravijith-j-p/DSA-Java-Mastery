Leetcode 70

Problem :
You are climbing a staircase.It takes n steps to reach the top
Each time you can climb is 1 or 2 steps
How mnay distict ways can you climb to the top ?

🔵 Example 1:
Input : n = 2
Output : 2

Explanation : 
1. 1 Step + 1 Step
2. 2 steps

🔵 Explanation 2:
Input : n = 3
Output : 3
Explanation :
1. 1step + 1step + 1step
2. 1step + 2 steps
3. 2 Steps + 1 step

💡 Intutuion 
At every step, you can come from either:
- one step before (n-1)
- two steps before (n-2)

So,

ways(n) = ways(n-1) + ways(n-2)

This is exactly like the fibonacci sequence

🔸 Brute Force - Recursive

                            class Solution{
                                public int climbStairs(int n){
                                    if(n <= 2) return n;
                                    return climbStairs(n-1) + climbStairs(n-2);
                                }
                            }
Time : O(2^n)
Space : O(n)

  ✅  Best Solution 
    Space-Optimized DP 

                                class Solution{
                                    public int climbStairs(int n){
                                        if(n <= 2) return n;
                                        int one = 1, two = 2;
                                        for(int i = 3; i<= n; i++){
                                            int curr = one + two;
                                            one = two;
                                            two = curr;
                                        }
                                        return two;
                                    }
                                }
Time : O(n)
Space : O(1)

