Leetcode 215

Problem :

Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

Can you solve it without sorting?

Example : 
Input : nums = [3, 2, 1, 5, 6, 4]
k = 2

Output  : 5

Explanation : Sorted array ->[1, 2, 3, 4, 5, 6] -> 2nd largest = 5

Approach 1 Min -Heap 

Time complexity : O(nlogk)
Space complexity : O(K)

Steps:
1. create a minheap (smallest element on top).
2. Traverse the array and add each element to the heap
3. If heap size exceeds k, remove the smallest element(poll()).
4. At the end, the root (top) of the heap is the kth largest element

import java.utils.*;

                                class Solution{
                                    public int findKthLargest(int[] nums, int k){
                                        PriorotyQueue<Integer> minHeap = new PriorityQueue<>();

                                        for(int num : nums){
                                            minHeap.add(num);
                                            if(minHeap.size() > k){
                                                minHeap.poll(); //remove smallest
                                            }
                                        }
                                        return minHeap.peek();
                                    }
                                }

