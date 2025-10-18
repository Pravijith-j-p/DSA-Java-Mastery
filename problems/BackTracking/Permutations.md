Leetcode 46

Given an array of distinct integers nums, return all possible permutations of the numbers
You can return the answer in any order

Example : 
nums = [1, 2, 3]
Output : [
    [1, 2, 3],
    [1, 3, 2],
    [2, 1, 3],
    [2, 3, 1],
    [3, 1, 2],
    [3, 2, 1]
]

❇️ Approach Backtracking 
1. Use a recursive function to explore permutations
2. Maintain a current path (list) and a boolean visited array to track which elements are already included
3. When the path length equals the array length, add it to the result
4. Backtrack by removing the last added element and marking it unvisited

import java.utils.*;

class Solution{
    public List<List<Integer>> permute(int []nums){
        List<List<Integer>> result = new ArrayList<>();
        boolean[]used = new boolean[nums.length];
        backtrack(nums, new ArrayList<>(), used, result);
        return result;
    }
    private void backtrack(int[]nums, List<Integer> current, boolean[] used, List<List<Integer>> result){
        if(current.size() == nums.length){
            result.add(new ArrayList<>(current));
            return;
        }

        for(int i =0;i< nums.length;i++){
            if(used[i]) continue;
            used[i] = true;
            current.add(nums[i]);
            backtrack(nums, current, used, result);
            current.remove(current.size() - 1);
            used[i] = false;
        }
    }
}

⏱️ Time & Space Complexity

Time: O(n * n!)
(There are n! permutations, each taking O(n) to copy into result)

Space: O(n) for recursion + O(n) for the used[] array.