⏳ What is time complexity ?

-> Time complexity is a way to measure how fast an alogorithm runs as the size of input grows.
-> Instead of actual time(ms or seconds),  we use number of steps the algorithm takes.
-> we express it in Big-O notation (O(1), O(n), O(logn), etc)

Think of it as : if input doubles, how much slower does my code get?


🔹 Common Complexities

|| Complexity     | Name        | Example                         | Growth    |
| -------------- | ----------- | ------------------------------- | ---------- |
| **O(1)**       | Constant    | Accessing `arr[i]`              | 🚀 Fastest |
| **O(log n)**   | Logarithmic | Binary search                   | Very fast  |
| **O(n)**       | Linear      | Looping through array           | Moderate   |
| **O(n log n)** | Log-linear  | Merge sort, Quick sort avg case | Efficient  |
| **O(n²)**      | Quadratic   | Nested loops                    | Slow       |
| **O(2ⁿ)**      | Exponential | Recursive Fibonacci             | Very slow  |
| **O(n!)**      | Factorial   | Traveling salesman brute force  | ❌ Worst   |

🔹 How to Understand It

Let's take an example in Java:

1. Constant time -> O(1)

    int [] arr = {1,2,3,4,5};
    System.out.println(arr[2]);    //Just 1 step

    //Always take 1 step, no matter if array size is 5 or 1 million

2. Linear Time → O(n)

    for (int i=0; i<n ; i++){
        System.out.println(i);
    }

    //if n = 10,loop runs 10 times
    // if n=1000, loop runs 1000 times

    💡 Complexity grows linearly with input.

3. Quadratic Time → O(n²)

    for (int i=0 ;i<n; i++){
        for(int j=0;j <n ;j++){
            System.out.println(i + " " + j);
        }
    }

   //if n =10, loop runs 100 times
   //if n=100, loop runs 10000 times

    💡 Nested loops → usually O(n²).

 4. Logarithmic Time → O(log n)   

    int binarySearch(int []arr, int target) {
        int low = 0, high = arr.length - 1;

        while(low <= high){
            int mid = low + high / 2;

            if (arr[mid] == target) return mid;
            else if (arr[mid] <  target) low = mid+1 ;
            else high = mid - 1;
        }
        return -1 ;
    }

    //Each step cuts input in half
    //id n=10,00,000, -> takes only 20 steps


🔹 Key Rule of Thumb

1. Count loops -> each loops = O(n)
2. Nested loops -> multiply (loop inside loop = O(n^2)).
3. Divide and conquer -> usually O(logn)or O(nlog n).
4. Ignore constants -> O(2n) = O (n), O(3n^2) = O(n^2).

✅ So: Time complexity = how input size affects number of operations.