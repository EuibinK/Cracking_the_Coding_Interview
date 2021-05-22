# VI. Big O

**Big O** - metric we use to describe the efficiency of algorithms

#### 

## Time Complexity

: ~(asymptotic runtime, or big O time)



### **Big O, Big Theta, and Big Omega**

- **O (Big O)** - upper bound on the time
  - e.g. an algorithm that prints all the values in an array - O(N), O(N^2)... etc
- **Ω (Big Omega)** - lower bound
  - e.g. an algorithm that prints all the values in an array - Ω(N), Ω(log N)... etc

- **θ (Big Theta)** - both O and ∆ - tight bound

  - " - θ(N)

    

**Tip**

- in industry, big O is closer to what academics mean by θ.

- try to offer the tightest description of the runtime



### Best Case, Worst Case, and Expected Case

: Let's think of a quick sort - picks a random element as a "pivot" and swaps values in the array such that the elements less than pivot appear before elements greater than pivot

- **Best Case** - if all elements are equal, then quick sort will just traverse through the array once - <u>O(N)</u>
- **Worst Case** - if the pivot is repeatedly the biggest element in the array - <u>O(N^2)</u>
- **Expected Case** - <u>O(N log N)</u>

 

**Tip**

- Best case is rarely discussed - not very useful concept
- In most cases, the worst case and the expected case are the same
- No particular relationship between best/worst/expected case <-> big O/theta/omega





## Space Complexity

































