Leetcode 704

Pattern: Binary Search (Classic)
Key Idea: Divide search space by half each time.

✅ Problem Summary

Given a sorted array nums and a target, return the index of target if it exists, otherwise return -1.

✅ Binary Search Intuition

Since the array is sorted, at every step:

Compare middle element mid with target.

If target < nums[mid] → search in left half.

If target > nums[mid] → search in right half.

If equal → return mid.

Time Complexity: O(log n)
Space Complexity: O(1) (iterative)

                            class Solution {
                                public int search(int[] nums, int target) {
                                    int left = 0;
                                    int right = nums.length - 1;

                                    while (left <= right) {
                                        int mid = left + (right - left) / 2;

                                        if (nums[mid] == target) {
                                            return mid;
                                        } else if (target < nums[mid]) {
                                            right = mid - 1;
                                        } else {
                                            left = mid + 1;
                                        }
                                    }

                                    return -1;
                                }
                            }
