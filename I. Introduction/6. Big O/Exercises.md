### Exercise 1

```java
int product(int a, int b) {
    int sum = 0;
    for (int i = 0; i < b; i++) {
        sum += a;
    }
    return sum;
}

// O(b)
```



### Exercise 2

```java
int power(int a, int b) {
    if (b < 0) {
        return 0; // error
    } else if (b == 0) {
        return 1;
    } else {
        return a * power(a, b - 1);
    }
}

// O(b)
```



### Exercise 3

```java
int mod(int a, int b) {
    if (b <= 0) {
        return -1;
    }
    int div = a / b;
    return a - div * b;
}

// O(1)
```



### Exercise 4

```java
int div(int a, int b) {
    int count = 0;
    int sum = b;
    while (sum <= a) {
        sum += b;
        count++;
    }
    return count;
}

// O(a/b)
```



### Exercise 5

```java
int sqrt(int n)
    return sqrt_helper(n, 1, n);
}

int sqrt_helper(int n, int min, int max) {
    if (max < min) return -1; // no square root
    
    int guess = (min + max) / 2;
    if (guess * guess == n) { // fount it!
    	return guess;
    } else if (guess * guess < n) { // too low
    	return sqrt_helper(n, guess+1, max);	// try higher
    } else { // too high
    	return sqrt_helper(n, min, guess-1); 	// try lower
    }
}

// O(log n)
```



### Exercise 6

```java
int sqrt(int n) {
    for (int guess = 1; guess * guess <= n; guess++) {
        if (guess * guess == n) {
            return guess;
        }
    }
    return -1;
}

// O(sqrt(n))
```



### Exercise 7

##### If a binary search tree is not balanced, how long might it take (worst case) to find an element in it?

- Worst case scenario:

  - Suppose we have n elements

  - Binary tree with depth = n

    --> **<u>O(n)</u>**



### Exercise 8

##### You are looking for a specific value in a binary tree, but the tree is not a binary search tree. What is the time complexity of this?

- Since the tree is not ordered, need to traverse through all existing nodes,

  --> **<u>O(n)</u>**



### Exercise 9

```java
int[] copyArray(int[] array) {
    int[] copy = new int[0];
    for (int value : array) {
        copy = appendToNew(copy, value);
    }
    return copy;
}

int[] appendToNew(int[] array, int value) {
    // copy all elements over to new array
    int[] bigger = new int[array.length + 1];
    for (int i = 0; i < array.length; i++) {
        bigger[i] = array[i];
    }
    
    // add new element
    bigger[bigger.length-1] = value;
    return bigger;
}

// O(n^2) <-- sum of 1 through n
```



### Exercise 10

```java
int sumDigits(int n) {
    int sum = 0;
    while (n > 0) {
        sum += n % 10;
        n /= 10;
    }
    return sum;
}

// O(log n)
```



### Exercise 11

```java
int numChars = 26;

void printSortedStrings(int remaining) {
    printSortedStrings(remaining, "");
}

void printSortedStrings(int remaining, String prefix) {
    if (remaining == 0) {
        if (isInOrder(prefix)) {
            System.out.println(prefix);
        }
    } else {
        for (int i = 0; i < numChars; i++) {
            char c = ithLetter(i);
            printSortedStrings(remaining-1, prefix+c);
        }
    }
}

boolean isInOrder(String s) {
    for (int i = 1; i < s.length(); i++) {
        int prev = ithLetter(s.charAt(i-1));
        int curr = ithLetter(s.charAt(i));
        if (prev > curr) {
            return false;
        }
    }
    return true;
}

char ithLetter(int i) {
    return (char) (((int) 'a') + i);
}


// O(k * 26^k)
	// takes O(26^k) to generate each string
	// need to check if each of these is sorted -- O(k)

// O(k) * O(26^k)
```



### Exercise 12

```java
int intersection(int[] a, int[] b) {
    mergesort(b);
    int intersect = 0;
    
    for (int x : a) {
        if (binearySearch(b, x) >= 0) {
            intersect++;
        }
    }
    
    return intersect;
}

// O(b log b) + O(a log b)
	// Sort array b -- O(b log b)
	// for each element in a, do binary search -- O(a log b)
```















