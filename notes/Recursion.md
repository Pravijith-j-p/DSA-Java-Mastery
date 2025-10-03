Definition : Recursion is when a function calls itself (directly or indirectly) to solve a problem

The idea is to break a big problem into smaller subproblems of the same type, solve them, and then combine reults

🔑 Key Parts of Recursion

1. Base Case - the stopping condition(prevents infinite calls)
2. Recursive Case - the function calls itself with smaller input

✅ Simple Example: Factorial

Mathematically:

                        n! = n × (n-1)!  
                        Base case: 0! = 1

                        Recursive Code
                        int factorial(int n) {
                            if (n == 0) return 1;      // base case
                            return n * factorial(n-1); // recursive case
                        }

