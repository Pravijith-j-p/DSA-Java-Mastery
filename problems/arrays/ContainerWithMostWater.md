LeetCode 11

Problem Statement:

You are given n non-negative integers height[i] where each represents a vertical line at coordinate i.
Find two lines that together form a container , such that the container holds the most water.
Return the maximum Area

Example : 

Input : height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
Output : 49
Explanation : the max area is between lines at index 1 and 8 (min(8,7) * (8-1)) = 7 * 7 = 49

🔹 Brute Force Approach

Check every pair of lines

                public int maxAreaBrute(int [] height){
                    int n = height.length;

                    int maxArea = 0;
                    for(int i = 0; i< n; i++){
                        for(int j = i+1; j<n; j++){
                            int area =Math.min(hieght[i], height[j]) * (j-1);
                            maxArea = Math.max(maxArea, area);
                        }
                    }
                    return maxArea;
                }

Time :O(n^2) -> too slow for large input
Space : O(1)

🔹 Optimized Approach: Two Pointers

- start with the left pointer at 0 and right pointer at n-1
- calculate area -> Math.min(hieght[left], height[right]) * (right - left)
- move the pointer poinitng to the smaller height(to possibly find the taller line)

                public int maxArea(int [] hieght){
                    int left = 0, right = height.length - 1 ;
                    int maxArea = 0;

                    while (left < right){
                        int area = Math.min (height[left], height[right]) * (right-left);
                        maxArea = Math.max(maxArea, area);

                        if(hieght[left] < hieght[right]){
                            left++;
                        }else{
                            right --;
                        }
                    }
                    return maxArea;
                }

Time : O(n)
Space : O(1)

🔹 Why Two Pointers Work?

Area depends on width × min height.

To maximize area, we need max width & taller lines.

If we move the taller line, width decreases and height won’t increase → wasted move.

Always move the smaller line.