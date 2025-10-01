Leetcode 560

Given : Integer array nums and integer k.Find the number of contigous subarrays whose sum equals k

Example : 

Input : nums = [1, 1, 1], k=2
Output  : 2


🔹 Brute Force Approach

Idea : check all subarrays and calculate their sum
if sum == k -> increment count

                public intsubarraySumBruteForce (int [] nums, int k){
                    int count = 0;
                    for(int i = 0;i < nums.length; i++){
                        int sum = 0;
                        for(int j = i; j< nums.length; j++){
                            sum += nums [j];
                            if (sum == k) count ++;
                        }
                    }
                    return count;
                }

Time complexity : O(n^2)
Space complexity : O(1) 

🔹 Optimized Approach: Prefix Sum + HashMap

Idea : maintain running sum ( prefix sum)
use a hasmap to count the frequency of prefix sum
for each element, check if (prefixSum - k) exists -> means subArray sum = k exists

                public int subArraySumOptimized (int [] nums , int k){
                    Map<Integer, Integer> map =new HashMap<>();
                    map.put(0, 1);  //base case
                    int count = 0, prefixSum = 0;

                    for(int num : nums){
                        prefixSum += num;

                        if(map.containsKey(prefixSum - k)){
                            count += map.get(prefixSum - k);
                        }

                        map.put(prefixSum, map.getOrDefault(prefixSum, 0) + 1);
                    }
                    return count;
                }
Time Complexity : O(n)
Space complexity : O(n)

🔹 Dry Run Example

        nums = [1, 1, 1], k = 2 

                | Index | Num | prefixSum | prefixSum - k | Map (prefix counts) | count |
                | ----- | --- | --------- | ------------- | ------------------- | ----- |
                | 0     | 1   | 1         | -1            | {0:1, 1:1}          | 0     |
                | 1     | 1   | 2         | 0             | {0:1,1:1,2:1}       | 1     |
                | 2     | 1   | 3         | 1             | {0:1,1:1,2:1,3:1}   | 2     |

                
