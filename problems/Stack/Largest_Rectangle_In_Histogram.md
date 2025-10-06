Leetcode 84

Problem : Given an array of integers heights, where each element represents the hieght of a bar in a histogram

return the area of the largest rectangle that can be formed within the histogram

Example 1 : 
Input : heights = [2, 1, 5, 6, 2, 3]
Output : 10
Explanation : The largest rectangle has area = 10 between heights 5 and 6

Example 2:
Input : heights = [2, 4]
Output : 4

🧠 Intution 
Each bar in the histogram can form a rectangle that extends
- to the left, until a shorter bar blocks it
- to the right, until a shorter bar blocks it

We want max area among all bars

🪜 Brute Force Approach
Idea:
For each bar i, expand left and right to find how far the rectangle can extend while all bars are >= heights[i]
Compute area = heights[i] * width

                        class BruteForceLargestRectangle{
                            public int largest RectangleArea(int[] heights){
                                int n = heights.length;
                                int maxArea = 0;

                                for(int i =0;i< n;i++){
                                    int minHeight = heights[i];

                                    for(int j = i;j<n;j++){
                                        minHeight = Math.min(minHeight, heights[j]);
                                        int width = j -i +1;
                                        maxArea = Math.max(maxArea, minheight*width);
                                    }
                                }
                                return maxArea;
                            }
                        }

Time complexity : O(n^2)
Space complexity : O(1)

✅ Optimized:  Monotonic Stack
Key Idea:
Use a stack to maintain indices of bars in increasing height order
when we find the bar shorter than the top of the stack:
We pop. from the stack and calculate the area of the rectangle using the popped hieght as the smallest bar


Steps:
1. use a stack to store indices
2. Traverse through all bars
    - while the current bar is shorter than the bar at stack top:
    - pop the top index
    - calculate the are of bar as:

    height  = heights[top]
    width = (stack empty) ? i : i -stack.peek() - 1
    area = height * width;
    Update maxArea
    push current index to stack
3. After the loop, pop all remaining bars and repeat the area calculation

import java.util.Stack;

                            class Solution{

                                public int largestReactangleArea(int [] heights){
                                    Stack<Integer> stack = new Stack<>();
                                    int maxArea = 0;
                                    int n = hieghts.length;

                                    for(int i=0;i<n;i++){
                                        int currHeight = (i ==n ) ? 0 : heights[i];

                                        while(!stack.isEmpty() && currHeight < heights[stack.peek()]){
                                            int height = heights[stack.pop()];
                                            int width = stack.isEmpty() ? i : i -stack.peek() -1;
                                            maxArea = Math.max(maxArea, height*width);
                                        }
                                        stack.push(i)
                                    }
                                    return maxArea;
                                }
                            }

Time Complexity : O(n)
Space Complexity : O(n)

⚙️ Pattern

Pattern: Monotonic Stack
Key Idea: Find Next Smaller to Left and Right using stack to calculate maximum rectangle area efficiently.