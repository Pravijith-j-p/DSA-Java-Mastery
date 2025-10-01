🔹 Definition of a String

A string is a sequence of characters stored in contiguous memory locations.
In Java , strings are represented by the String class in java.lang package

Strings in java are immutable , meaning once astring object is created , its value cannot be changed
 - Any modification (like concatenation, replacement) actually creates a new String object
 For mutable strings (where we want to change the content withour creating new objects), Java provides:
  - StringBuilder -> not thread-safe, but faster
  - StringBuffer -> thread-safe, but slightly slower.

  (Thread-safe - A piece of code or object is thread-safe if it can be safely used by multiple threads at the same time without causing data corruption or unexpected behavior)

  Thread : A lightweight unit of execution in a program (like a mini - program running concurrently).
  Problem without thread-safety : if two Threads try to modify the same data simulataneously, you might get incorrect results or exceptions.

  