 Problem Two Sum

 Statement:
 Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

 Example:

 Input: nums = [2,7,11,15], target = 9
 Output: [0,1]
 Explanation: nums[0] + nums[1] = 2 + 7 = 9, so return [0, 1].

 🔹 Brute Force Approach
 check all pairs using nested loops:

---------------------------------------
    for (int i=0; i< nums.length; i++){
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) {
                return new int[]{i, j};
            }
        }
    }
---------------------------------------

 Time Complexity: O(n^2) -> too slow for large inputs
 Space Complexity: O(1) -> no extra space used

 🔹 Optimized Approach : HashMap Pattern
 Use a HashMap to store the complement values and their indices:

 A hash table or hashmap is a data structure that helps with mapping key to values for highly efficient operations like the lookup, insertion and deletion operations.

Idea : 
 -> While traversing the array, store each number in a Hashmap along with it's index.
 -> For the current number num, check if target - num exists in map
    * if yes -> solution found
    * if no -> add num to the map and continue

Why it works:
-> Hashmap allows O(1) loopup, so we only traverse the array once -> O(n) time
---------------------------------------

    import java.util.HashMap;

    public class TwoSum {

    public int [] twoSum (int []nums, int target){
        HaspMap<Integer, Integer> map = new HasMap<>;   //num -> index

        for(int i=0; i<nums.length; i++>){
            int complement = target - nums[i];          //what we need to find

            if(map.containsKey(complement)){
                return new int []{map.get(complement), i };
            }

            return new int [] {};                       //if no solution
        }
    }
}
---------------------------------------

Let's visualise for better understanding

nums = [ 2, 7, 11, 15] , target = 9 

Step 1 : Initialize Hashmap
map = {}

Step 2 : First iteration (i=0)
current number : 2
complement : 9 - 2 =7       
check map : not in map
Add 2 to map:
    map = {2: 0}                //number : index

Step 3 : Second Iteration (i = 1)
Current number: 7
complement : 9 - 7 = 2
check map : 2 is in map
Solution found ✅

indices = [map.get(2), 1] = [0, 1]

Step 4 : Stop
return [0, 1]

Hashmap now contains all numbers seen so far:
map = { 2; 0, 7:1 } 


ANALYSIS

Time  -> O(1) - traverse array once
Space -> O(n) - store upto n elements in HashMap


Pattern reusable:

--->Two numbers sum / difference / complement problems

--->Subarray sum with prefix sum + HashMap

--->Frequency counting

Two Sum Variants:

Leetcode : 167
------------------

- Input array is sorted 
- use two pointers instead of Hashmap
- Time : O(n) Space : O(1)

       public int [] two SumSorted(int [] numbers, int target) {
           int left = 0, right = numbers.length - 1;
           while (left < right){
               int sum = numbers[left] + numbers[right];
               if (sum == target) return new int [] {left+1, right+1};         //1 - indexed
               elseif (sum < target) left ++ ;
               else right -- ;
           }
           return new int [] {};
       }

Two Sum IV - input is a BST

Leetcode :  653
------------------

-- Input is a binary Search Tree
-- Use haset while doing DFS
-- Time: O(n), Space:O(n)


Question : you are given a root of BST and an integer k.
Task : Return true if there exist two elements in the BST such that their sum equals k.

This is basically two sum in arrays , but now the input is structured as a tree:
- instead of iterating through an array, we traverse the BST
- Use a HashSet to store seen values
- for each node, check:
    if(k - node.val ) is already in the set -> pair found
    otherwise, add node.val to the set and continue DFS.


      public boolean findTarget(Treenode root, int k){
          HashSet<Integer> set =new HashSet<>();
          return dfs(root, k, set);
      }
      
      private boolean dfs(TreeNode node, int k, HashSet<Integer> set){
          if(node == null) return false;
          if(set.contains(k - node.val)) return true;
          set.add(node.val);
          return dfs(node.left, k, set) || dfs(node.right, k, set);
      }


EXAMPLE:

   5
   / \
  3   6
 / \    \
2   4    7

input k = 9

- visit 5 -> store {5}
- visit 3 -> store {5, 3}
- visit 2 -> store {5, 3, 2}
- visit 4 -> complement = 9 - 4 =5 ->found




                                    ┌─────────────┐
                                    │   Two Sum   │
                                    │  LeetCode 1 │
                                    └─────┬───────┘
                                        │
                            ┌──────────────┴───────────────┐
                            │                              │
                ┌───────────────┐                ┌───────────────┐
                │  Unsorted     │                │   Sorted      │
                │  Array        │                │  Array        │
                │  HashMap      │                │ Two Pointers  │
                └───────────────┘                └───────────────┘
                            │                              │
                - Traverse array once             - Initialize left & right pointers
                - Store complement → index       - Sum = nums[left] + nums[right]
                - Check map.contains             - Move pointers based on sum
                - O(n) time, O(n) space         - O(n) time, O(1) space

                            │
                ┌────────┴─────────┐
                │  BST / Tree      │
                │  Two Sum IV      │
                │  LeetCode 653    │
                └────────┬─────────┘
                            │
                - DFS traversal
                - HashSet to store visited node values
                - Check if (k - node.val) exists
                - O(n) time, O(n) space


