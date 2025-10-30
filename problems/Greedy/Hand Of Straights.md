Leetcode 846

Problem: 

Given:

hand: array of card values

groupSize: size of each consecutive group

Goal:
Return true if the cards can be rearranged into groups of size groupSize,
where each group consists of consecutive integers.

Example:
hand = [1,2,3,6,2,3,4,7,8], groupSize = 3 → ✅ true
You can form: [1,2,3], [2,3,4], [6,7,8]

✅ Key Idea (Greedy + Sorting or TreeMap)
✅ 1. If total cards not divisible by groupSize → impossible

Because every group must have exactly groupSize cards.

✅ 2. Use a frequency map (TreeMap)

TreeMap keeps keys sorted, so you always start forming groups from the smallest available number.

✅ 3. For each smallest number x, try to form sequence:
x, x+1, x+2, ..., x + groupSize - 1


If any required number is missing → return false.

Example Walkthrough
Input

hand = [1,2,3,6,2,3,4,7,8]
groupSize = 3

Sorted map:
1,2,2,3,3,4,6,7,8

Start with 1 → need {1,2,3}
Then next smallest left is 2 → need {2,3,4}
Then 6 → need {6,7,8}

✅ Completed → true

class Solution {
    public boolean isNStraightHand(int[] hand, int groupSize) {
        if (hand.length % groupSize != 0) return false;
        
        TreeMap<Integer, Integer> map = new TreeMap<>();
        
        for (int card : hand) {
            map.put(card, map.getOrDefault(card, 0) + 1);
        }
        
        while (!map.isEmpty()) {
            int first = map.firstKey();  // smallest value
            
            for (int i = 0; i < groupSize; i++) {
                int curr = first + i;
                
                if (!map.containsKey(curr)) 
                    return false;
                
                map.put(curr, map.get(curr) - 1);
                
                if (map.get(curr) == 0)
                    map.remove(curr);
            }
        }
        
        return true;
    }
}

| Complexity | Value                                  |
| ---------- | -------------------------------------- |
| **Time**   | O(n log n) (due to TreeMap operations) |
| **Space**  | O(n)                                   |
