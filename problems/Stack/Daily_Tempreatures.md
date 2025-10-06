Leetcode 739

Given an integer array temperatures where tempreatures[i] represents the daily temperature on day[i]

Return an array answer such that answer[i] is the number of days you have to wait after the ith day to get a warmer temperature

If there is no future day for which this is possible, set answer[i]

Example : 
Input : tempratures = [73, 74, 75, 71, 69, 72, 76, 73]
Output : [1, 1, 4, 2, 1, 1, 0, 0]

Input : tempreatures = [30, 40, 50, 60]
Output : [1, 1, 1, 0]

Example 3: 
Input : tempreatures = [30, 60, 90]
Output : [1, 1, 0]


🧠 Intuition
This is a Next Greater Element problem.

For each day, you need to find:
- The next day where tempreature is greater than current

A brute force approach would compare each element with all future elements ->O(n^2)
But we can do better with a monotonic decreasing stack

🪜 Brute Force Approach
🔸 Idea : 
For each day i,scan all future days j > i until you find a warmer tempreature

                                class BruteForceDailyTempreatures{
                                    public int [] dailyTempreatures(int [] tempreatures){
                                        int n = tempreatures.length;
                                        int [] ans = new int[n];

                                        for(int i=0;i<n;i++){
                                            for(int j=i+1;j<n;j++){
                                                if(tempreature[j] > tempreature[i]){
                                                    ans[i] = j - i;
                                                    break;
                                                }
                                            }
                                        }
                                        return ans;
                                    }
                                }
Time : O(n^2)
Space : O(1)

✅ Optimal Solution
Monotonic stack

- Use a stack that store indices of days maintaining a monotonicall decreasing stack of tempreatures

Steps : 
- Traverse tempreatures from left to right
- While current temperature T[i] is greater than that of at the tops index of stack
    - pop the index prev
    - calculate ans[prev] = i - previous (days waited)
- push current index i to stack
- remaining indices in the stack have no warmer days 0-> by default

                            import jav.util.Stack;

                            class Solution{
                                public int[] dailyTempreatures(int[] tempreatures){
                                    int n = tempreatures.length;
                                    int [] ans = new int[n];
                                    Stack<Integer> stack = new Stack<>();

                                    for(int i = 0;i<n;i++){
                                        while(!stack.isEmpty()&& tempreatures[i]>tempreature[stack.peek()]){
                                            int prev = stack.pop();
                                            ans[prev] = i - prev;
                                        }
                                        stack.push(i);
                                    }
                                    return ans;
                                }
                            }

Time complexity : O(n)
Space Complexity : O(n)

