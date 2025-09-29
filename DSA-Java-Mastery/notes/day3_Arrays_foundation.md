📦 Arrays – The Foundation

1. What is an Array?

    Definition : A collection of elements of the same type stored in contiguous memory locations.
    Key Feature: Supports random access -> we can directly access any element using its index.

Example :
                int [] arr = {10, 20, 30, 40, 50}
                System.out.println(arr[2]);         //Output 30

2. Why are arrays important?

    Arrays form the base of Strings, Hashing, Matrices, Heaps, DP tables, etc.
    Many problems (sliding window, two pointers, prefix sums) are built on arrays.


3. Basic operations on Arrays

| Operation                        | Time Complexity | Explanation                |
| -------------------------------- | --------------- | -------------------------- |
| Access (arr[i])                  | **O(1)**        | Direct index lookup        |
| Search (linear)                  | **O(n)**        | Check each element         |
| Insert at end (amortized)        | **O(1)**        | If space available         |
| Insert/Delete at arbitrary index | **O(n)**        | Requires shifting elements |

4. Common Array Problems

-- Traversals -
    loop thought the array -> base for all problems

                for(int i =0;i< arr.length; i++){
                    System.out.print(arr[i] + "");
                }

-- Reverse an array -
    Swap elements from both ends.
    Time : O(n) , Space O(1).

-- Find Maximum and Minimum
    Single pass -> Time :O(n)

-- Rotate an array
    Right/left rotation
    Optimized using reverse method

-- Subarray Problems
    Maximum Subarray Sum (Kadane's Algorithm)
    prefix sums for range quries

-- Two pointer technique
    works on sorted arrays
    two sum ||, trapping rainwater

-- Sliding window
    fixed or variable size window
    example :maximum sum subarray of size k , longest subarray without repeating characters.


5️⃣ Patterns You Must Master in Arrays

        Brute Force → Optimized (always show interviewer both).

        Two Pointers → shrinking/expanding windows.

        Prefix Sum / Difference Array → range queries.

        Hashing with Arrays/Maps → frequency counts.

        Binary Search on Arrays → foundation for advanced problems.




    