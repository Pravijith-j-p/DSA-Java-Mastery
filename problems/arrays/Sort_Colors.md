LeetCode 75

Problem :
You are given an array nums with n objects colored red(0), white(1), or blue(2).
Sort them in-place so that objects of the same color are adjacent, with colors in the order red-> white ->blue.
- you must not use the built in sort
- must do it in O(n) time and O(1) space ideally.

🔹 Brute Force (Counting Sort)

Idea:
Count the number of 0s,1s, and 2s.

Rewrite the array with that many 0s,1s,2s

Steps :
- Travserse the array once -> count occurences
- Rewrite the array accordingly

                        public void sortColors(int []nums){
                            int count  =0, count1 =0, count2 = 0;

                            for(int num:nums){
                                if(num == 0) count0++;
                                else if(num == 1) count1++;
                                else count2++;
                            }

                            int i = 0;
                            while (count0-- > 0) nums[i++] = 0;
                            while (count1-- > 0) nums[i++] = 1;
                            while (count2-- > 0) nums[i++] = 2;
                        }
Time complexity : O(n)
Space complexity : O(1)

🔹 Optimal Approach (Dutch National Flag Algorithm)
Idea :
Use three pointers:
- low -> position for next 0
- mid -> position for next 1
- high -> position for next 2
 
Traverse array once, swapping elements to thier correct position

Steps :
1. Initialize low =0;mid = 0;high = nums.length - 1;
2. While mid <= high:
    - if (nums[mid] == 0) ->swap with low, move both
    - if (nums[mid] == 1) -> just move mid
    - if (nums[mid] == 2) -> swap with high, move high (not mid)

                            public void sortColors(int [] nums){
                                int low=0,mid=0,high= nums.length -1;

                                while(mid<= high){
                                    if(nums[mid] == 0){
                                        swap(nums, low, mid);
                                        low ++;
                                        mid ++;
                                    }else if (nums[mid] == 1){
                                        mid ++;
                                    }else{
                                        swap(nums, mid, high)
                                        high--;
                                    }
                                }
                            }
                            private void swap(int[] nums, int i, int j){
                                int temp = nums[i];
                                nums[i] = nums[j];
                                nums[j] = temp;
                            }

Time complexity : O(n)
Space complexity : O(1)