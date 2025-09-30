LeetCode 42

Problem Statement 

Given n non-negative integers representing the elevation map (where each bar's width = 1), compute how much water it can trap after raining

Example 
 
input : height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]
Output : 6
Explanation : The trapped water is at indices [2, 4, 5, 6, 8, 10]

🔹 Brute Force

For each index :
- find max height on left 
- find max hieght on right
- water trapped at i = min(maxLeft, maxRight) - height [i]

                public int trapBrute(int[] height){
                    int n = height.length, water =0;
                    for(int i = 0; i< n; i ++){
                        int leftMax =0 , rightMax = 0;
                        for(int l= 0; l<= i; l++) leftMax = Math.max(leftMax, height[l]);
                        for(int r= 0; r< n; r++) rightMax = Math.max(rightMax, height[r]);
                        water += Math.min(leftMax, rightMax) - height[i];
                    }
                    return water;
                }

Time : O(n^2)
Space : O(1)

🔹 Optimized with Prefix & Suffix

- Precompute leftMax [i] = tallest bar from left up to i
- precompute rightMax [i] = tallest bar from right upto i
- Water [i] = min(leftMax[i], rightMax[i] - height[i])

                public int trapPrefixSuffix(int [] height){
                    int n = height.length;
                    int [] leftMax = new int [n];
                    int [] rightMax = new int [n];

                    leftMax[0] = height[0];
                    for(int i = 1;i< n;i++){
                        leftMax [i] = Math.max(leftMax[i - 1], height[i]);
                    } 

                    rightMax [n -1] = height [n-1];
                    for(int i = n-2; i > = 0; i--) {
                        rightMax [i] = Math.max( maxRight [i+1], height [i]);
                    }

                    int water = 0;
                    for(int i = 0; i < n; i++){
                        water += Math.min(leftMax[i], rightMax[i] - height[i]);
                    }
                    return water;
                }

 Time : O(n)
 Space : O(n)

 🔹 Optimal Two Pointers

 - Use left and right pointers
 - track leftMax and rightMax
 - whichever side is smaller decides the water trapped

                    public int trap(int[] height) {
                        int left = 0, right = height.length - 1;
                        int leftMax = 0, rightMax = 0, water = 0;
                        
                        while (left < right) {
                            if (height[left] < height[right]) {
                                if (height[left] >= leftMax) {
                                    leftMax = height[left];
                                } else {
                                    water += leftMax - height[left];
                                }
                                left++;
                            } else {
                                if (height[right] >= rightMax) {
                                    rightMax = height[right];
                                } else {
                                    water += rightMax - height[right];
                                }
                                right--;
                            }
                        }
                        return water;
                    }
Time :O(n)
Space : O(1)

