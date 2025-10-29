Leetcode 74

✅ Problem Summary

You are given an m x n matrix where:

Each row is sorted

The first element of each row is greater than the last element of the previous row

This means the matrix behaves like one big sorted array.

Your task: return true if target exists, else false.

✅ Intuition

Because the matrix is sorted like a 1D array, you can apply binary search on the entire matrix.

Flattened index mapping:

index → row = index / n
index → col = index % n


Where n = number of columns.

                                class Solution {
                                    public boolean searchMatrix(int[][] matrix, int target) {
                                        int m = matrix.length;
                                        int n = matrix[0].length;

                                        int left = 0;
                                        int right = m * n - 1;

                                        while (left <= right) {
                                            int mid = left + (right - left) / 2;

                                            int row = mid / n;
                                            int col = mid % n;

                                            if (matrix[row][col] == target) {
                                                return true;
                                            } else if (matrix[row][col] < target) {
                                                left = mid + 1;
                                            } else {
                                                right = mid - 1;
                                            }
                                        }

                                        return false;
                                    }
                                }
Example : 

matrix = [
  [1,3,5,7],
  [10,11,16,20],
  [23,30,34,60]
]
target = 3 → true  
target = 13 → false

Time: O(log(m*n))
Space: O(1)