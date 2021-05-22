### Example 1

What is the runtime of the below code?

```java
void foo(int[] array) {
    int sum = 0;
    int product = 1;
    
    for (int i = 0; i < array.length; i++) {
        sum += array[i];
    }
    
    for (int i = 0; i < array.length; i++) {
        product *= array[i];
    }
    System.out.println(sum + ", " + product);
}

// O(N)
```



### Example 2

What is the runtime of the below code?

```java
void printPairs(int [] array) {
    for (int i = 0; i < array.length; i++) {
        for (int j = 0; j < array.length; j++) {
            System.out.println(array[i] + "," + array[j]);
        }
    }
}

// O(N^2) --> doubly nested for loops
```



### Example 3

```java
void printUnorderedPairs(int[] array) {
    for (int i = 0; i < array.length; i++) {
        for (int j = i + 1; j < array.length; j++) {
            System.out.println(array[i] + "," + array[j]);
        }
    }
}

// loops N(N-1)/2 times --> O(N^2)
```



### Example 4

```java
void printUnorderedPairs(int[] arrayA, int[] arrayB) {
	for (int i = 0; i < arrayA.length; i++) {
        for (int j = 0; j < arrayB.length; j++) {
            if (arrayA[i] < arrayB[j]) {
                System.out.println(arrayA[i] + "," + arrayB[j]);
            }
        }
    }
}

// suppose a = arrayA.length, b = arrayB.length
// O(ab)
```



### Example 5

```java
void printUnorderedPairs(int[] array A, int[] arrayB) {
    for (int i = 0; i < arrayA.length; i++) {
        for (int j = 0; j < arrayB.length; j++) {
            for (int k = 0; k < 100000; k++) {
                System.out.println(arrayA[i] + "," + arrayB[j]);
            }
        }
    }
}

// Since 100,000 is still constant, O(ab)
```



### Example 6

```java
void reserve(int[] array) {
    for (int i = 0; i < array.length / 2; i++) {
        int other = array.length - i - 1;
        int temp = array[i];
        array[i] = array[other];
        array[other] = temp;
    }
}

// Still degree of O(N)
```



###  Example 7

Which of the following are equivalent to O(N)? Why?

- **O(N + P), P < N/2**
- **O(2N)**
- **O(N + log(N)**
- <u>O(N + M) ≠ O(N)</u>
  - don't have detailed info about M



### Example 8

Suppose we had an algorithm that took in an array of strings, sorted each string, and then sorted the full array. What would the runtime be?

- Let **s** be the length of the longest string, and let **a** be the length of the array
  - Sorting each string => O(s log s)
    - Repeat for every string => **<u>O(a * s log s)</u>**
  - Sort all the strings => O(a log a)
  - **Need to compare the strings**
    - Each string comparison => O(s)
      - Perform O(a log a) comparisons => <u>**O(s * a log a)**</u>
- Hence, total time complexity would be **O(a * s (log a + log s))**



### Example 9

Balanced binary search tree

```java
int sum(Node node) {
    if (node == null) {
        return 0;
    }
    return sum(node.left) + node.value + sum(node.right)
}

// O(N)
```

- Since the runtime of a recursive function with multiple branches --> O(branches ^ depth)
  - and for binary trees, we have 2 branches each --> O(2 ^ depth)
    - Since we're dealing with a balanced binary tree, if we start off with N nodes, depth ~ log N
      - O(2 ^ log N) = **O(N)**



### Example 10

```java
boolean isPrime (int n) {
    for (int x = 2; x * x <= n; x++) {
        if (n % x == 0) {
            return false;
        }
    }
    return true;
}

// O(sqrt(n)) --> Since we're looping sqrt(n) times
```



### Example 11

```java
int factorial(int n) {
    if (n < 0) {
        return -1;
    } else if (n == 0) {
        return 1;
    } else {
        return n * factorial (n - 1);
    }
}
    
// Recursively call n times --> O(n)
```



### Example 12 (Challenging, prob. beyong the scope of internship interview)

```java
void permutation(String str) {
    permutation(str, "");
}

void permutation(String str, String prefix) {
    if (str.length() == 0) {
        System.out.println(prefix);				// O(n) -- each char needs to be printed
    } else {
        for (int i = 0; i < str.length(); i++) {
            String rem = str.substring(0, i) + str.substring(i + 1);
            permutation(rem, prefix + str.charAt(i));
            // L10+11: O(n) -- string concatenation
        }
    }
} // Each call takes O(n) time combined

// Total run time ==> O(n * n!) * O(n) = O(n^2 * n!)
```



### Example 13

```java
int fib(int n) {
    if (n <= 0) return 0;
    else if (n == 1) return 1;
    return fib(n - 1) + fib(n - 2);
}

// 2 branches per call, go deep as N --> O(2^N)
	// For bonus points, mention that the actual run time would be far less than O(2^n)
	// since at the bottom of the call stack, there may be only one call 
```



### Example 14

```java
void allFib(int n) {
    for (int i = 0; i < n; i++) {
        System.out.println(i + ": " + fib(i));
    }
}

int fib(int n) {
    if (n <= 0) return 0;
    else if (n == 1) return 1;
    return fib(n - 1) + fib(n - 2);
}

// Suppose we start with allFib(n)
/*
	fib(1) -> 2^1 steps
	fib(2) -> 2^2 steps
	fib(3) -> 2^3 steps
	...
	fib(n) -> 2^n steps
  --> Total: 2^(n+1) --> O(2^n)
*/
```



### Example 15

Fibonacci Numbers being stored in an integer array

```java
void allFib(int n) {
    int[] memo = new int[n + 1];
    for (int i = 0; i < n; i++) {
        System.out.println(i + ": " + fib(i, memo));
    }
}

int fib(int n, int[] memo) {
    if (n <= 0) return 0;
    else if (n == 1) return 1;
    else if (memo[n] > 0) return memo[n];
    
    memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
    return memo[n];
}

/*
  fib(1) -> return 1
  fib(2)
  	fib(1) -> return 1
  	fib(0) -> return 0
  	store 1 at memo[2]
  fib(3)
  	fib(2) -> lookup memo[2] -> return 1
  	fib(1) -> return 1
  	store 2 at memo[3]
  fib(4)
  	fib(3) -> lookup memo[3] -> return 2
  	fib(2) -> lookup memo[2] -> return 1
  	store 3 at memo[4]
  ...
  
  ==> Takes O(n)
*/
```



### Example 16

Prints the power of 2 from 1 through n (e.g. n = 4 => prints 1 2 4)

```c++
int powersOf2(int n) {
    if (n < 1) {
        return 0;
    } else if (n == 1) {
        cout << 1 << endl;
        return 1;
    } else {
        int prev = powersOf2(n / 2);
        int curr = prev * 2;
        cout << curr << endl;
        return curr;
    }
}
// O(log n)
```



















































