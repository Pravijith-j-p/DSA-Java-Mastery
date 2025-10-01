Leetcode : 15

Problem : Given an integer array nums, find all unique triplets [a, b, c] such that a+b+c = 0

1️⃣ Brute Force Approach

Idea : Check all triplets (i, j, k) using 3 nested loops
Time Complexity  : O(n^2)
Space Complexity : O(1)

                public class ThreeSumBruteForce {
                    public List<List<Integers>> threeSum(int [] nums) {
                        List<List<Integer>> result = new ArrayList<> ();
                        int n = nums.length;
                        Arrays.sort(nums);  //optional skips duplicates later
                        for(int i = 0;i < n-2; i++){
                            for(int j = i+1;j < n -1; j++){
                                for(int k = j+1; k< n; k++){
                                    if(nums[i] + nums[j] + nums[k] == 0){
                                        List<Integer> triplet = Arrays.asList(nums[i], nums[j], nums[k]);
                                        if(! result.contains(triplet)) // skip duplicates
                                        result.add(triplet);
                                    }
                                }
                            }
                        }
                        return result;
                    }
                }

2️⃣ Optimized Approach (Two Pointers)

Idea : Sort the array
For each nums[i], use two pointers left and right to find pairs such that nums[i] + nums[left] + nums[right] = 0
skip duplicates to ensure unique triplets

Time Complexity : O(n^2)
Space complexity : O(1)

                    public class ThreeSumOptimized{
                        public List<List<Integers>> threeSum(int [] nums){
                            List<List<Integers>> result = new ArrayList<> ();
                            Arrays.sort(nums);      //sort first
                            for(int i = 0; i< nums.length - 2; i++){
                                if(i > 0 && nums[i] == nums[i - 1]) continue;  //skip duplicates

                                int left = i +1;
                                int right = nums.length - 1;

                                while (left < right){
                                    int sum = nums[i] + nums[left] + nums[right];

                                    if(sum == 0){
                                        result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                                        left ++;
                                        right --;
                                        //skip duplicates

                                        while (left < right && nums[left] == nums[left - 1]) left ++;
                                        while (left < right && nums[right] == nums[right + 1]) right --;
                                    }else if (sum < 0){
                                        left++;
                                    }else{
                                        right --;
                                    }
                                }
                            }
                            return result;
                        }
                    }

Example :
nums = [-1, 0, 1, 2, -1, -4]

sorted: [-4, -1, -1, 0, 1, 2]

- triplets found :[-1, -1, 2] , [-1, 0, 1]