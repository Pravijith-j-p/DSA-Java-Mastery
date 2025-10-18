Leetcode 90

Problem :
Given an integer array nums that may contain duplicates, return all possible unique subsets (the power set).

The solution must not contain duplicate subsets

Example : 
Input : nums = [1, 2, 2]

Output : 
[
    [],
    [1],
    [2],
    [1, 2],
    [2, 2],
    [1 ,2, 2]
]

Approach - Backtracking with duplicate Handling

1. Sort the array -  this ensures duplicate are adjacent
2. Use backtracking to explore all inclusion/exclusion combinations
3. Skip duplicates - when you see the same number twice in the same recursive level (avoid identical subsets).

import java.utils.*;

                    class Solution{
                        public List<List<Integers>> subsetsWithDup(int[] nums) {
                            List<List<Integer>> result = new ArrayList<>();
                            Arrays.sort(nums);
                            backtrack(nums, 0, new ArrayList<>(), result);
                            return result;
                        }
                        private void backtrack(int[] nums, int start, List<Integer> current, List<List<Integer>>result){

                            result.add(new ArrayList<>(current));

                            for(int i =start; i< nums.length;i++){
                                if(i>start && nums[i] == nums[i - 1]) continue;

                                current.add(nums[i]);
                                backtrack(nums, i+1, current, result);
                                current.remove(current.size() - 1);
                            }
                        }
                    }

⏱️ Complexity

Time: O(2^n) (every element can be included/excluded, minus duplicates)

Space: O(n) recursion stack + output storage.