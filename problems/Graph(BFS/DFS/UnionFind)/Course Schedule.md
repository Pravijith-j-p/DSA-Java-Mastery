Leetcode 207

Problem : 
Given 
- numCourses : total number of courses labeled 0 -> numCourses - 1
- prerequisites[i] = [a, b] means:
    - to take course a, you must first take b

Return true if you can finish all courses (i.e., no cycle exists), otherwise false

🔹 Example 1

Input:

numCourses = 2
prerequisites = [[1,0]]


Output: true
✅ You can take course 0, then course 1.

🔹 Example 2

Input:

numCourses = 2
prerequisites = [[1,0],[0,1]]


Output: false
❌ There’s a cycle (0 → 1 → 0).

🧠 Concept

This is a cycle detection in a directed graph problem.

If there’s no cycle, topological ordering exists → all courses can be finished.

If there’s a cycle, it’s impossible to complete all.

⚙️ Two Main Approaches
🩵 1. DFS (Recursive Cycle Detection)

Use 3 states for each node:

0 → Not visited

1 → Visiting (currently in recursion stack)

2 → Fully visited (safe)

If we visit a node that’s already 1 (in recursion), that means a cycle exists.

class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < numCourses; i++)
            graph.add(new ArrayList<>());

        // Build adjacency list
        for (int[] pre : prerequisites) {
            graph.get(pre[1]).add(pre[0]);
        }

        int[] state = new int[numCourses]; // 0=unvisited, 1=visiting, 2=visited

        for (int i = 0; i < numCourses; i++) {
            if (state[i] == 0 && hasCycle(graph, state, i)) {
                return false;
            }
        }
        return true;
    }

    private boolean hasCycle(List<List<Integer>> graph, int[] state, int course) {
        if (state[course] == 1) return true;  // Found cycle
        if (state[course] == 2) return false; // Already processed

        state[course] = 1; // Mark as visiting
        for (int next : graph.get(course)) {
            if (hasCycle(graph, state, next)) return true;
        }
        state[course] = 2; // Mark as done
        return false;
    }
}

Time complexity : O(v + E)
Space complexity : O(V + E)

