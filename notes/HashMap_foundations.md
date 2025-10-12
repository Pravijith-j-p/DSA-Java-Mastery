HashMap is a key-value pair data structure that allows fast access, insertion and deletion of data typically in O(1) time.

It worjs kuje a dictionary:
- Each key maps to a specific value
- Keys are unique
- Values can be duplicate

⚙️ How it works (Conceptually)
1. Every key is passed through a hash function,
   which converts it into a numeric value called a hash code
2. This has code determines the index (bucket) in an internal array where the value is stored
3. When you need ti retrieve a value using a key ,
   the same has function find sthe cirrect bucket in constant time

Example : 
| Key     | Value |
| ------- | ----- |
| "India" | 91    |
| "USA"   | 1     |
| "UK"    | 44    |

Here ,
- "India" is the key
- 91 is the value

Example in Java

import java.utli.*;


                            public class Example{
                                public static void main(String [] args){

                                    //Create a HashMap
                                    HashMap<String , Integer> map = new HashMap<>();

                                    //Insert a (key, value) pairs
                                    map.put("India", 91);
                                    map.put("USA", 1);
                                    map.put("UK", 44);

                                    //Retrieve a value using key
                                    System.out.println(map.get("India"))        //Output : 91

                                    //Check if a key exists
                                    System.out.println(map.containsKey("UK"));  //true

                                    //Remove a key
                                    map.remove("USA");

                                    //Iterate over a key value pairs
                                    for(Map.Entry<String, Integer> entry : map.entrySet()){
                                        System.out.println(entry.getKey() + " -> " +enrty.getValue());
                                    }
                                } 
                            }


📦 Internal Working (Simplified)
-A HashMap is made up of:

- An array of buckets (linked lists or trees)

- Each bucket stores nodes that contain:

    - key

    - value

    - hash

    - next (pointer to next node, in case of collision)

🌀 When Collisions Occur

If two keys generate the same hash index:

They are stored in the same bucket (as a linked list or balanced tree).

In Java 8+, if many collisions occur, it switches from a linked list → Red-Black Tree for better performance.

Time Complexities

| Operation | Average Case | Worst Case                             |
| --------- | ------------ | -------------------------------------- |
| Insertion | O(1)         | O(n) (if all keys hash to same bucket) |
| Deletion  | O(1)         | O(n)                                   |
| Search    | O(1)         | O(n)                                   |


❇️ Important HashMap Methods:

| Method                        | Description               |
| ----------------------------- | ------------------------- |
| `put(K key, V value)`         | Add key-value pair        |
| `get(Object key)`             | Get value by key          |
| `remove(Object key)`          | Delete key-value pair     |
| `containsKey(Object key)`     | Check if key exists       |
| `containsValue(Object value)` | Check if value exists     |
| `size()`                      | Number of key-value pairs |
| `clear()`                     | Remove all entries        |


                          