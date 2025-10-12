A HashSet is a collection that stores unique elements only - no duplicates allowed
It is based on the HashMap internally

Think of it as a bag where you can toss in items , but if you try to add a duplicate, it's automatically ignored

⚙️ How HashSet works internally
- Internally, HashSet uses a HashMap
- Each element you add to the HashSet becomes a key in the HashMap
- the values for all entries is a constant dummy object(PRESENT).

so when you do :
set.add("Apple");

Under the hood it's doing
map.put("Apple", PRESENT);

If apple already exists, it won't be added again(since keys in a HashMap are unique).

Example :

import java.utils.*

                            public class Example{
                                public static void main(String[] args){
                                    HashSet<String> set = new HashSet<>();

                                    //Add elements
                                    set.add("Apple");
                                    set.add("Banana");
                                    set.add("Cherry");
                                    set.add("Apple");   //Duplicate ignored

                                    //Print the set
                                    Syste.out.println(set);

                                    //check if an element exists
                                    System.out.println(set.contains("Banana"));  //true

                                    //Remove an element
                                    set.remove("Cherry");

                                    //Iterate over elements
                                    for(String s :set){
                                        System.out.println(s);
                                    }

                                    //Size of the set
                                    System.out.println("Size" + set.size());
                                }
                            }

⚡ Key Characteristics

| Feature           | Description                                     |
| ----------------- | ----------------------------------------------- |
| **Duplicates**    | Not allowed                                     |
| **Null**          | One `null` element allowed                      |
| **Order**         | Not maintained (unlike `LinkedHashSet`)         |
| **Underlying DS** | Uses `HashMap`                                  |
| **Performance**   | O(1) average time for add, remove, and contains |

🧠 Important Methods

| Method               | Description                           |
| -------------------- | ------------------------------------- |
| `add(E e)`           | Adds element (if not already present) |
| `remove(Object o)`   | Removes element if present            |
| `contains(Object o)` | Checks if element exists              |
| `size()`             | Returns number of elements            |
| `clear()`            | Removes all elements                  |
| `isEmpty()`          | Checks if set is empty                |

🧩 Variants of Set in Java

| Set Type          | Description                                            |
| ----------------- | ------------------------------------------------------ |
| **HashSet**       | Fast, unordered, uses hashing                          |
| **LinkedHashSet** | Maintains insertion order                              |
| **TreeSet**       | Sorted order (based on natural ordering or comparator) |
