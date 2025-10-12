Leetcode 347

Problem :
Given an integer array nums and an integer k , return the k most frequent elements.
You can return the answer in any order

Example : 
Input : nums =[1, 1, 1, 2, 2, 3] , k = 2
Output : [1 , 2]
Explanation : 1 appears 3 times, 2 appears 2 times and 3 appears once -> top 2 frequent = [1, 2]

Approach 1 - Using HashMap + MinHeap (Priority Queue)

Time complexity : O(n log k)
Space complexity : O(N)

Steps : 
- Count the fequency of each number using HashMap
- Use a min-heap (Prioroty Queue) of size k to store elements by frequency
- if heap size exceeds k, remove the element with the smallest frequency
- finally , extract all elements from the heap


