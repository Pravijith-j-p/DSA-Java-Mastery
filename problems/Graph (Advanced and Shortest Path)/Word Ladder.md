Leetcode 127

Problem : 
Given 
- beginWord
- endWord
- wordList

Each transformation must :

✅ Change exactly one letter
✅ Result in a valid word from wordList

Your goal:

Find the shortest transformation sequence length from beginWord to endWord.

If no sequence exists → return 0.

✅ Why BFS?

We need the shortest path in an unweighted graph.
Each word represents a node; edges exist if they differ by 1 letter.

➡️ Shortest path in unweighted graph = BFS

✅ Preprocessing Trick (Very Important)

To efficiently get neighbors (words that differ by one letter), build generic patterns:

For "hot":

*ot

h*t

ho*

Mapping pattern → words:

*ot → hot, dot, lot
h*t → hot, hit
ho* → hot


This makes neighbor lookup O(1).

                    class Solution {
                        public int ladderLength(String beginWord, String endWord, List<String> wordList) {

                            Set<String> wordSet = new HashSet<>(wordList);
                            if (!wordSet.contains(endWord)) return 0;

                            Map<String, List<String>> patternMap = new HashMap<>();

                            // Build pattern dictionary
                            for (String word : wordSet) {
                                for (int i = 0; i < word.length(); i++) {
                                    String pattern = word.substring(0, i) + "*" + word.substring(i + 1);
                                    patternMap.computeIfAbsent(pattern, k -> new ArrayList<>()).add(word);
                                }
                            }

                            // BFS
                            Queue<String> q = new LinkedList<>();
                            q.add(beginWord);

                            Set<String> visited = new HashSet<>();
                            visited.add(beginWord);

                            int steps = 1;

                            while (!q.isEmpty()) {
                                int size = q.size();

                                while (size-- > 0) {
                                    String word = q.poll();
                                    if (word.equals(endWord)) return steps;

                                    for (int i = 0; i < word.length(); i++) {
                                        String pattern = word.substring(0, i) + "*" + word.substring(i + 1);

                                        if (patternMap.containsKey(pattern)) {
                                            for (String nei : patternMap.get(pattern)) {
                                                if (!visited.contains(nei)) {
                                                    visited.add(nei);
                                                    q.add(nei);
                                                }
                                            }
                                        }
                                    }
                                }
                                steps++;
                            }

                            return 0;
                        }
                    }

Time complexity : O(n * L^2)
Space complexity : O(n*l)

