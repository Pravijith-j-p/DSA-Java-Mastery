Leetcode 208

Problem 
Design a data structure called Trie (or prefix tree) that supports the following operations:
1. insert(word) - inserts a word into the trie
2. search(word) - returns true if word is there in trie
3. startsWith(prefix) - returns true if there is any word in the trie that starts with the given prefix


A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.


Exmaple :
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple"); //return true
trie.search("app"); //returns false
trie.startsWith("app") //return true
trie.insert("app") 
trie.search("app")  //returns true

🔵 Brute force approach
Idea:
Use a simple ArrayList or HashSet to store all inserted words
- for search, check if the word exists in the collection
- for startsWith , iterate through all words and check if any word starts with the prefix

Time complexity :
insert : O(1) for adding word
search : O(n*k) 
startsWith : O(n*k)

Space complexity : O(n*k)

✅ Optimized approach(Trie)

Idea ;
Use a tree structure where each node contains :
- children :Map of charcters to child nodes
- isEndOfWord : Boolean flag to mark the end of a word

This allows O(k) time for insert, search, and startsWith, where k = length of the word

                                    class TrieNode{
                                        Map<Character, TrieNode> children = new HashMap<>();
                                        boolean isEndOfWord = false;
                                    }
                                    class Trie{
                                        private TrieNode root;

                                        public Trie(){
                                            root = new TrieNode();
                                        }
                                        //Insert a word
                                        public void insert (String word){
                                            TrieNode node = root;
                                            for(char c : word.toCharArray()){
                                                node.children.putIfAbsent(c, new TrieNode());
                                                node = node.children.get(c);
                                            }
                                            node.isEndOfWord = true;
                                        }
                                        //Search a word
                                        public boolean search(String word){
                                            TrieNode node = root;
                                            for(char c : word.toCharArray()){
                                                if(!node.children.containsKey(c)) return false;
                                                node = node.children.get(c);
                                            }
                                            return node.isEndOfWord;
                                        }
                                        //Search prefix
                                        public boolean startsWith(String prefix){
                                            TrieNode node = root;
                                            for(char c: prefix.toCharArray()){
                                                if(!node.children.containsKey(c)) return false;
                                                node = node.children.get(C);
                                            }
                                            return true;
                                        }
                                    }

Pattern / Key Idea

Tree-based prefix storage

DFS / iterative traversal per word

Efficient for large dictionaries / autocomplete / prefix search

Time Complexity:

insert, search, startsWith → O(k)
Space Complexity:

O(n * k) → each character in each word may need a node