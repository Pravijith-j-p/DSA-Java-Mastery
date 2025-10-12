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

                                import java.utils.*

                                class Solution{
                                    public int [] topKFrequent(int[] nums, int k){
                                        //Step 1 : Count frequencies
                                        Map<Integer, Integer> freqMap = new HashMap<>();
                                        for(int num : nums){
                                            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
                                        }

                                        //Step 2 : Use a min heap (Priority Queue) sorted by frequency
                                        PriorityQueue<>((a, b) -> a.getValue() - b.getValue());

                                        for(Map.Entry<Integer, Integer> entry: freqMap.entrySet()){
                                            minHeap.add(entry);
                                            if(minHeap.size() > k){
                                                minHeap.poll();     //remove last frequent
                                            }
                                        }

                                        //Step 3: Extract top k elements
                                        int[] result = new int[k];
                                        for(int i = k-1;i>= 0;i--){
                                            result[i] = minHeap.poll().getKey();
                                        }
                                        return result;
                                    }
                                }

Apporach 2 - Using Bucket Sort

1. use a HashMap to count frequencies
2. Create buckets where bucket[i] contains elements that appear i times
3. Traverse from high frequency to low and collect top k elements

                                    import java.util.*;

                                    class Solution {
                                        public int[] topKFrequent(int[] nums, int k) {
                                            Map<Integer, Integer> freqMap = new HashMap<>();
                                            for (int n : nums)
                                                freqMap.put(n, freqMap.getOrDefault(n, 0) + 1);

                                            // Create buckets
                                            List<Integer>[] bucket = new List[nums.length + 1];
                                            for (int key : freqMap.keySet()) {
                                                int freq = freqMap.get(key);
                                                if (bucket[freq] == null) bucket[freq] = new ArrayList<>();
                                                bucket[freq].add(key);
                                            }

                                            // Collect top K elements
                                            List<Integer> result = new ArrayList<>();
                                            for (int i = bucket.length - 1; i >= 0 && result.size() < k; i--) {
                                                if (bucket[i] != null) result.addAll(bucket[i]);
                                            }

                                            return result.stream().mapToInt(i -> i).toArray();
                                        }
                                    }

