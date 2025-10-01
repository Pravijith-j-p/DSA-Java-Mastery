Leetcode 33

Given : A sorted array nums rotated at some pivot (unknown)
An integer target

Task : Return the index of target in nums
if not found , return -1

Example : 

Input : nums = [4, 5, 6, 7, 0, 1, 2] , target = 0
Output : 4

Pattern /Key Idea

Modified Binary Search
Array is partially sorted due to rotation
Check which part is sorted and decide whether to search left or right

Optimized approach O((logn))

                            public int search[int [] nums, int target] {
                                int left = 0, right = nums.length - 1 ;

                                while (left <= right) {
                                    int mid = left + (right - left) / 2;

                                    if(nums[mid] == target ) return mid;

                                    //Left side is sorted
                                    if(nums[left] < = nums[mid]) {
                                        if(target > = nums[left] && target < nums[mid])
                                            right = mid -1;
                                        else
                                            left = mid + 1;
                                    }
                                    //Right side is sorted
                                    else {
                                        if(target > nums[mid] && target < = nums[right])
                                        left = mid + 1;
                                        else 
                                            right = mid - 1;
                                    }
                                }
                                return -1;
                            }