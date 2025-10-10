Leetcode 211

Problem : 
Design a data structure that supports adding new words and searching for strings - including searches with the . wildcard, where . can represent any letter

Must implement two methods :
- void addWord(String word)
- boolean search(String word)

Example :
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");

wordDictionary.search("pad");  //false
wordDictionary.search("bad");  //true
wordDictionary.search(".ad");  //true
wordDictionary.search("b..");  //true

🔵 Brute Force Approach
Idea : 
Store all words in a List or Set
When Searching:
- if no . present-> simple lookup
- if .present -> check every stored word if it matches pattern character by character

                                class WordDictionary{
                                    List<String> words = new ArrayList<>();

                                    public void addWord(String word){
                                        words.add(word);
                                    }
                                    public boolean search(String word){
                                        for(String w : words){
                                            if(isMatch(w, word)) return true;
                                        }
                                        return false;
                                    }
                                    private boolean isMatch(String a, String b){
                                        if(a.length() != b.length()) return false;
                                        for(int i = 0;i<a.length;i++){
                                            if(b.charAt(i) != '.'c&& a.charAt(i) != b.charAt(i)) return false;
                                        }
                                        return true;
                                    }
                                }

Time complexity : O(1)
Search ; O(n*m)(n->words, m->length)

✅ Optimized approach (Trie + DFS)
Idea: 
We use a Trie (prefix tree) but modify search logic:
- if the current character is a normal letter -> move to the corresponding child
- if the current charcter is '.' -> recursively explore all children at that level

                            class TrieNode {
                                TrieNode[] children = new TrieNode[26];
                                boolean isEndOfWord = false;
                            }

                            class WordDictionary {
                                private TrieNode root;

                                public WordDictionary() {
                                    root = new TrieNode();
                                }

                                // Add a word to the trie
                                public void addWord(String word) {
                                    TrieNode node = root;
                                    for (char c : word.toCharArray()) {
                                        int index = c - 'a';
                                        if (node.children[index] == null) {
                                            node.children[index] = new TrieNode();
                                        }
                                        node = node.children[index];
                                    }
                                    node.isEndOfWord = true;
                                }

                                // Search with support for '.'
                                public boolean search(String word) {
                                    return dfsSearch(word, 0, root);
                                }

                                private boolean dfsSearch(String word, int index, TrieNode node) {  // fixed variable name
                                    if (node == null) return false;
                                    if (index == word.length()) return node.isEndOfWord;  // now valid

                                    char c = word.charAt(index);
                                    if (c == '.') {
                                        for (TrieNode child : node.children) {
                                            if (child != null && dfsSearch(word, index + 1, child)) {
                                                return true;
                                            }
                                        }
                                        return false;
                                    } else {
                                        return dfsSearch(word, index + 1, node.children[c - 'a']);
                                    }
                                }
                            }
