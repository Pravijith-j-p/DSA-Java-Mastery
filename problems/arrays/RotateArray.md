LeetCode 189

Given an array nums and an integer k , rotate the array to the right by k steps, where k is non-negative.

Example 1:

    Input : nums = [1, 2, 3, 4, 5, 6, 7] , k=3
    Output : [5, 6, 7, 1, 2, 3, 4]

    Explanation:
    rotate 1 step -> [7, 1, 2, 3, 4, 5, 6]
    rotate 2 step -> [6, 7, 1, 2, 3, 4 ,5]
    rotate 3 step -> [5, 6, 7, 1, 2, 3, 4]

Example 2:

    Input : nums = [-1, -100, 3, 99] , k = 2
    Output : [ 3, 99, -1, -100]

    Constraints :
        Rotate in-place, ideally O(1) extra space
        k can be larger than array length (k = k%n)

🔹 Brute Force Approach

    Rotate one step at a time, repeat k times
    Time Complexity: O(n * k) ->slow for large arrays
    Space Complexity: O(1)

            for(int i = 0; i< k; i++){
                int last = nums [nums.length - 1];
                for (int j = nums.length-1; j>0; j--){
                    nums [j] = nums [j - 1];
                }
                nums [0] = last;
            }
🔹 Optimized Approach (Reverse Method)

Idea :
- Reverste the entire array 
- Reverse the first k elements
- Reverse the remaining n-k elements

            public void rotate(int [] nums, int k){
                int n = nums.length;
                k = k % n;  //incase k>n

                reverse(nums, 0, n-1);
                reverse(nums, 0, k-1);
                reverse(nums, 0, n-1);
            }

            public void reverse(int [] nums, int start, int end){
                while (start < end){
                    int temp = nums[start];
                    nums[start] = nums [end];
                    nums [end] = temp;
                    start ++;
                    end --;
                }
            }

🔹 Edge Cases

k = 0 → no rotation

k = n → same array

Array length = 1 → no rotation

k > n → use k % n