Leetcode 4

Goal: Find the median of two sorted arrays in O(log(min(n, m))).

✅ Intuition / Why This Is Hard

Merging both arrays is easy (O(n + m)), but the question restricts us to:

✅ O(log(min(n, m))) time
✅ No merging

So the only approach that works is Binary Search on Partitions.

✅ Key Idea — Partitioning

We want to partition the two sorted arrays so that:

left side has exactly half (or half+1) of the numbers
right side has the rest


Let arrays be:

A = nums1 (size m)
B = nums2 (size n)


Always binary search on the smaller array.

We choose a partition i in A
Then partition j in B is forced:

j = (m + n + 1)/2 - i


We check if partition is valid:

A[i-1] <= B[j]
B[j-1] <= A[i]


If not:

If A[i-1] > B[j] → move left

Else → move right

✅ Final Median Rule

If total count is odd:

median = max(A[i-1], B[j-1])


Else:

median = (max(A[i-1], B[j-1]) + min(A[i], B[j])) / 2

class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        // Ensure nums1 is smaller
        if (nums1.length > nums2.length)
            return findMedianSortedArrays(nums2, nums1);

        int m = nums1.length;
        int n = nums2.length;

        int low = 0, high = m;

        while (low <= high) {
            int i = (low + high) / 2;
            int j = (m + n + 1) / 2 - i;

            int leftA  = (i == 0) ? Integer.MIN_VALUE : nums1[i - 1];
            int rightA = (i == m) ? Integer.MAX_VALUE : nums1[i];

            int leftB  = (j == 0) ? Integer.MIN_VALUE : nums2[j - 1];
            int rightB = (j == n) ? Integer.MAX_VALUE : nums2[j];

            // Valid partition
            if (leftA <= rightB && leftB <= rightA) {
                if ((m + n) % 2 == 0) {
                    return ((double)Math.max(leftA, leftB) + Math.min(rightA, rightB)) / 2.0;
                } else {
                    return (double)Math.max(leftA, leftB);
                }
            }

            // Move left
            if (leftA > rightB) {
                high = i - 1;
            } else {
                // Move right
                low = i + 1;
            }
        }

        return 0.0; // Should never reach here
    }
}

| Operation | Complexity            |
| --------- | --------------------- |
| Time      | **O(log(min(n, m)))** |
| Space     | **O(1)**              |
