Leetcode 269

✅ Problem Summary

You are given a sorted list of words from an alien language.
The goal is to determine the order of characters in this alien alphabet.

Example:

["wrt", "wrf", "er", "ett", "rftt"]


You must deduce the correct ordering, e.g.:

"wertf"


If no valid ordering exists (graph has cycle) → return "".

✅ Pattern / Key Idea
Topological Sort on a Directed Graph

Build graph of character precedence

Compare each pair of adjacent words

Find the first differing character:

word1[i] != word2[i]
→ create edge word1[i] → word2[i]


This gives ordering constraints.

Invalid Case
If word1 starts with word2 (prefix case), e.g.:

["abc", "ab"]


→ No possible ordering → return "".

Perform topological sort

Compute in-degree of each character

Use Kahn’s BFS:

Push chars with 0 in-degree

Pop, append to result

Reduce in-degree of neighbors

If result length != number of unique chars → Cycle → return ""

                            class Solution {
                                public String alienOrder(String[] words) {

                                    Map<Character, Set<Character>> graph = new HashMap<>();
                                    Map<Character, Integer> indegree = new HashMap<>();

                                    // Step 1: Initialize all characters in indegree map
                                    for (String w : words) {
                                        for (char c : w.toCharArray()) {
                                            indegree.put(c, 0);
                                            graph.putIfAbsent(c, new HashSet<>());
                                        }
                                    }

                                    // Step 2: Build edges from adjacent word comparisons
                                    for (int i = 0; i < words.length - 1; i++) {
                                        String w1 = words[i];
                                        String w2 = words[i + 1];

                                        // invalid case
                                        if (w1.length() > w2.length() && w1.startsWith(w2))
                                            return "";

                                        int len = Math.min(w1.length(), w2.length());
                                        for (int j = 0; j < len; j++) {
                                            char c1 = w1.charAt(j);
                                            char c2 = w2.charAt(j);

                                            if (c1 != c2) {
                                                if (!graph.get(c1).contains(c2)) {
                                                    graph.get(c1).add(c2);
                                                    indegree.put(c2, indegree.get(c2) + 1);
                                                }
                                                break; // first mismatch defines ordering
                                            }
                                        }
                                    }

                                    // Step 3: Topological Sort (Kahn’s BFS)
                                    Queue<Character> q = new LinkedList<>();
                                    for (char c : indegree.keySet()) {
                                        if (indegree.get(c) == 0) q.offer(c);
                                    }

                                    StringBuilder sb = new StringBuilder();

                                    while (!q.isEmpty()) {
                                        char curr = q.poll();
                                        sb.append(curr);

                                        for (char nei : graph.get(curr)) {
                                            indegree.put(nei, indegree.get(nei) - 1);
                                            if (indegree.get(nei) == 0) q.offer(nei);
                                        }
                                    }

                                    // If not all characters included → cycle
                                    if (sb.length() != indegree.size()) return "";

                                    return sb.toString();
                                }
                            }

Time complexity : O(N * L)
Space complexity : O(V + E)

