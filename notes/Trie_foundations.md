A trie is a tree-like data structure that stores a dynamic set of strings, usually to optimize searching.
- Each node represents a charcter
- The path from root to node represents a prefix of one or more strings
- Leaf Nodes or nodes with a special marker indicate the end of a valid word.

🌳 Structure

For words : ["cat", "car", "dog"]

Trie looks like this
                                                (root)
                                                  / \
                                                c    d
                                               /\     \
                                              a  a     o
                                              |  |     |
                                              t  r     g
cat -> path : root->c->a->t
car -> path : root->c->a->r
dog -> path : root->d->o->g

⚙️ Operations

| Operation            | Description                          | Time Complexity          |
| -------------------- | ------------------------------------ | ------------------------ |
| `insert(word)`       | Add a word to the trie               | O(L), L = length of word |
| `search(word)`       | Check if word exists                 | O(L)                     |
| `startsWith(prefix)` | Check if any word starts with prefix | O(L)                     |
| `delete(word)`       | Remove word from trie                | O(L)                     |



🧩 PART 1 — TrieNode class
class TrieNode {
    TrieNode[] children = new TrieNode[26]; // a-z
    boolean isEndOfWord;

    TrieNode() {
        isEndOfWord = false;
        for(int i=0; i<26; i++)
            children[i] = null;
    }
}
-------------------------------------------------------------
🔵 What it does:
Each node in the trie represents a charcter
- TrieNode[] children = new TrieNode[26];   ->each node has 26 possible children, one for each lowercase English letter 'a' to 'z' (index 0-> 'a' , 1-> 'b', .....25->'z')
- boolean isEndOfWord;          -> This flag tells whether this node marks end of a valid word(for example 't' in "cat")
Constructor :
TrieNode(){
    isEndOfWord = false;
    for(int i = 0;i<26;i++)
    children[i] = null;
}
-> when a node is created, none of its 26 child links exist yet (all are null)
-> its also not the end of the word
So each Trienode can lead to 26 other letters - just like branches in a word tree

-------------------------------------------------------------
class Trie {
    TrieNode root;

    Trie() {
        root = new TrieNode();
    }

🔵 What it does:
- Trie is the main class that uses TrieNode to build the full tree.
- It starts with a root node, which is empty (it doesnot represnt any letter)
- Every word you insert will start from this root
-------------------------------------------------------------
    void insert(String word) {
        TrieNode node = root;
        for(char ch : word.toCharArray()) {
            int index = ch - 'a';
            if(node.children[index] == null)
                node.children[index] = new TrieNode();
            node = node.children[index];
        }
        node.isEndOfWord = true;
    }

🔵 Start from the root
- for each charcter ch in "cat"
 - Compute index -> c - 'a' = 2
 - if node.children[2] == null, create a new node
 - move node to that child
- After processing 't', mark isEndOfWord = true
-------------------------------------------------------------
    boolean search(String word) {
        TrieNode node = root;
        for(char ch : word.toCharArray()) {
            int index = ch - 'a';
            if(node.children[index] == null) return false;
            node = node.children[index];
        }
        return node.isEndOfWord;
    }

🔹 What it does:
Checks if a word exists in the Trie.

Example: Searching "car"

Go from root → c → a → r

If all characters exist, and last node (r) has isEndOfWord = true, return true.

If a letter’s child doesn’t exist or the last node isn’t end-of-word → return false.
-------------------------------------------------------------
    boolean startsWith(String prefix) {
        TrieNode node = root;
        for(char ch : prefix.toCharArray()) {
            int index = ch - 'a';
            if(node.children[index] == null) return false;
            node = node.children[index];
        }
        return true;
    }
}


🔹 What it does:
Checks if there is any word starting with a given prefix.