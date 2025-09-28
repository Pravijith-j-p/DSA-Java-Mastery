🔹 What is Space Complexity?

Space complexity measures the amount of memory an algorithm uses with respect to input size

It includes:

1. Fixed part -> memory for constants,program instructions, compiler overhead.
2. Variable part -> memory used by variables, functions calls, recursion stack, and data structures.

So basically:
     
        ---> Space Complexity = Fixed Part + Variable Part <---

        Examples in Java:

        1. Constant Space → O(1)

            class Example{
                public static void main(String [] args){
                    int a = 5 ;     //constant space
                    int b = 10;
                    int sum = a + b;
                    System.out.println(sum);
                }
            }

            ✅ Always uses the same memory regardless of input size → O(1).

        2.  Linear Space → O(n)

            class Example{
                public static void main(String [] args){
                    int n = 5 ;
                    int [ ] arr = new int [ n ];
                    for (int i =0 ; i< n ;i++){
                        arr[i] = i*i;
                    }
                }
            }

            ✅ Uses memory proportional to n (array) → O(n).

        3. Recursive Calls -> Stack space

            class Factorial{

                static int fact(int n ){
                    if (n == 0) return -1;
                    return n * fact(n-1);
                }

                public static void main(String [ ] args){
                    System.out.println(fact(5));
                }
            }    

            //Each recursive call adds a new frame to the stack.
            //For fact(n) , stack depth = n.
            //Space complexity =O(n) (Stack memory).


🔹 Common Space Complexities

O(1) → Constant memory (variables, math ops).

O(n) → Arrays, linked lists, recursion depth.

O(n²) → 2D matrix, adjacency matrix.

O(log n) → Divide & conquer recursion (like binary search).            


💡 Key Idea:

If an algorithm only uses a few variables → O(1).

If it stores all inputs (array, list, etc.) → O(n).

If it uses recursion, add stack memory to calculation.