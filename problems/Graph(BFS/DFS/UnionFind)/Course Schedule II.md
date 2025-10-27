Leetcode 210

Problem :
Given :
 - numCourses -> total number of courses labeled 0 to numCourses-1
 - prerequisites[i] = [a, b] -> to take a, you must first take b

Return : 
- An order of courses you can take to finish all courses
- If impossible (due to a cycle), return an empty array.

Example 1:
Input : 
numCourses = 4
prerequisites = [[1, 0], [2, 0], [3, 1], [3, 2]]

Output : 
[0, 2, 1, 3]

Exaplanation
Course 0 first -> 1 and 2 next-> 3 last
(Any valid order like [0, 1, 2, 3] also works)

)

🧠 Concept

Same as LeetCode 207 (Course Schedule), but instead of just checking for a cycle,
we must also produce a topological ordering (a valid sequence of course completion).

⚙️ Approach — BFS (Kahn’s Algorithm)

Build graph (adjacency list) and in-degree array.

Add all nodes with inDegree = 0 to a queue.

Pop one course at a time → add it to result list.

Reduce in-degree of its dependent courses.

If a dependent course reaches inDegree = 0, add it to queue.

If all courses processed → return result.

Else → cycle exists → return empty array.

                        class Solution {
                            public int[] findOrder(int numCourses, int[][] prerequisites) {
                                List<List<Integer>> graph = new ArrayList<>();
                                int[] indegree = new int[numCourses];

                                // Initialize adjacency list
                                for (int i = 0; i < numCourses; i++)
                                    graph.add(new ArrayList<>());

                                // Build graph and indegree
                                for (int[] pre : prerequisites) {
                                    int course = pre[0];
                                    int prereq = pre[1];
                                    graph.get(prereq).add(course);
                                    indegree[course]++;
                                }

                                Queue<Integer> queue = new LinkedList<>();
                                for (int i = 0; i < numCourses; i++) {
                                    if (indegree[i] == 0)
                                        queue.offer(i);
                                }

                                int[] order = new int[numCourses];
                                int index = 0;

                                while (!queue.isEmpty()) {
                                    int curr = queue.poll();
                                    order[index++] = curr;

                                    for (int next : graph.get(curr)) {
                                        indegree[next]--;
                                        if (indegree[next] == 0)
                                            queue.offer(next);
                                    }
                                }

                                // If all courses processed → return order
                                if (index == numCourses)
                                    return order;
                                else
                                    return new int[0]; // cycle detected
                            }
                        }
Time complexity : O(V + E)
Space complexity : O(V + E)