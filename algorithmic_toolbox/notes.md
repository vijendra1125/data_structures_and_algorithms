# Overview
* week1:
  * Introduction
  * Programming challenges
  * Stress testing
* week2:
  * Fibonacci number
  * Greatest common divisor
  * Big-O notation
* week3:
  * Greedy algorithm
* week4:
  * Divide and conquer
* week5:
  * Dynamic programming
* week6:
  * Dynamic programming

# Week 1
## Testing:
* Test on the examples from the problem statement.
* Make a few other small test, solve them manually and check that your program output the correct answer. 
* Generate a big input and launch your program to check that it works fast enough and doesn’t consume too much memory. 
* Test for corner cases: smallest allowed value and largest allowed value (for integer overflow) of all input parameters, equal numbers in the input, verylong strings etc.
* Make stress test (comparison between naive and implementation to be considered with generated random inputs).


# Week 2

## Fibonacci numbers: 
* $F_{n} = 0 \;\;if \;n = 0, \newline\;\;\;\;\;
= 1 \;\;if \;n = 1, 
\newline\;\;\;\;\;
= F_{n-1} + F_{n-2} \;\;if \;n > 1$

* Fibonacci number grows as fast as power of 2, for eaxmple $F_{30}$ is over a million and $F_{100}$ already have 21 digits. In general 
  > $F_{n} > ~ 2^{0.649\,n}$

* Pisano period: 
  * For any integer $m≥2$, the sequence $F_{n}$ mod m is periodic. The period always starts with *"0 1"* and is known as Pisano period. 
  * Using above, in order to calculate caclate $F_{n}$ mod m where n is very large:
    * Find pisano period length for 'mod m' by finding index where *"0 1"* appears again while claculating mod
    * Divide n by pisano period length of 'mod m' to get reminder r, $F_{r}$ mod m will be equal to $F_{n}$ mod m
* Note:
        (a+b)%n = ((a%n) + (b%n)) % n <- use it with property of fibonacci
        number ($F_{n} = F_{n-1} + F_{n-2}$) and it will help you many fibonacci numbers problems

## Gereatest Common Divisor:
* For integers $a$ and $b$, $gcd(a,b)$ is greatest integer which divides both. 
* Lemma: Let $a'$ be the reminder when a is divided by b, then 
> $gcd(a,b) = gcd(b, a') = gcd(a', b)$

## Program's runtime complexity:
* Runtime depends on program and system used to run it. Increament because of system related factors like speed of computer, system architecture, compiler being used and detail of memory hirerarchy etc. is not so straight forward to calcuate but it multiply runtime by a (large) constant. so we need a method to measure runtime which ignore constant multiples.

* Asymptotic runtime measures how runtime scale with input size. 

* Below shows relative scaling of most useful ones for runtime measurement:
> $log(n) > \sqrt{n} > n > n.log(n) > n^2 > 2^n$

* Big-O Notation: 
  * $f(n) = O(g(n))$ is read as $f$ is Big-O $g$ and represents that $f(n)$ scales slower in compare to g(n) if there exist constants N and c so that for all $n >= N$, $f(n) <= c.g(n)$. 
  

  * Common rules of Big-O notation:
    * Multiplicative constant could be omitted 
    * Leave lower order term which becomes less significant as n grows and hence $5n^2 + 3n + 2$ becomes $O(n^2)$.
    * Note that growth rate of $5n^2 + 3n + 2$ is same as $n^2$
    * In order to keep bigger picture, we treat two functions equivalent if they differ only by multiplicative constant such that $f1/f2 <= constant1 \newline and \newline f2/f2 <= constant2$ 
  * Benefit of using Big-O notation: 
    * Clarifies growth-rate
    * Cleans up notation
    * Can ignore system related complicated details as its asymptotic
  * Cons definetily include that we lose detail of measured runtime 
* Other notations: 
  * As Big-O denotes <= 
  * $\Omega$ denotes >=
  *  $\Theta$ denotes ==

* Other runtime measurement notes:
  * Addition of n-bit number takes time roughly propotional to n

* Useful logarithms for runtime measurement:
> $log_{a}(n^k) = k.log_{a}(n) \newline
log_{a}(n.m) = log_{a}(n) + log_{a}(m) \newline
n^{log_{a}(b)} = b^{(log_{a}(n)} \newline
log_{n}(a) . log_{b}(a) = log_{b}(n)$

## Additional Reading resource:
* Sanjoy Dasgupta, Christos Papadimitriou, and Umesh Vazirani. Algorithms (1stEdition). McGraw-Hill Higher Education. 2008.
  * Computing Fibonacci numbers: Section 0.2
  * Properties of Fibonacci numbers: Exercises 0.2–0.4
  * Greatest common divisor: Section 1.2.3
  * Big-O notation and growth rate: Section 0.3
* Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, Clifford Stein. Introduction to Algorithms (3rd Edition). MIT Press and McGraw-Hill. 2009.
  * Greatest common divisor: Section 31.2

# Week 3
## Greedy Algorith
* General strategy for greedy algorithm:
  * Come up with a greedy choice
  * Prove that this greedy choice is safe move (there is an optimal solution consistent with the first move)
  * Reduce to subproblem (a simillar problem of smaler size) 
  * Solve the subproblem by going back to step 1

## Additional Reading Resource:
* Gilles Brassard and Paul Bratley. Fundamentals of Algorithms. Prentice-Hall. 1996.
  * Knapsack: Section 6.5

# Week 4
## Divide and Conquer
### Strategy
  * Break into non-overlaping subproblems that are themselfs smaller instance of same type of problem
  * Recursively solve the subproblems
  * Appropriately combine results

### Recurrence relation
  * A Recurrence relation is an equation recursively defining a sequence of value
  * Divide-and-conquer algorithms often follow a generic pattern: they tackle a problem of size n by recursively solving, say,a subproblems of size n/b and then combining these answers in $O(n^d)$ time, for some a;b;d > 0. Their running time can therefore be captured by the equation 
  > $T(n) = aT({\lceil}(n/b){\rceil}) + O(n^d)$

### Master theorm
  * Provides recurrance relation to find runtime complexity of most of the divide-and-conquer procedures:
  If $\newline T(n) = aT({\lceil}(n/b){\rceil}) + O(n^d) \newline$ 
  for some constant a>0; b>1; d>=0. Then,
  $T(n) = O(n^d) \;if\; d > log_{b}(a)
  \newline \;\;\;\;\;\;\;\;\;
  = O(n^d log(n)) \;if\; d = log_{b}(a) 
  \newline \;\;\;\;\;\;\;\;\;
  = O(n^(log_{b}(a))) \;if\; d <log_{b}(a)$
  * Advance master theorm: 
  https://www.geeksforgeeks.org/advanced-master-theorem-for-divide-and-conquer-recurrences/

### Linear search:
* Sequential search made over all item one-by Recurrence relation defining
* Worst case runtime: 
        T(n) = T(n-1) + c
* Runtime complexity: O(n)

### Binary search: 
* Works if data is in sorted form. 
* Binary search looks for a particular item by comparing the middle most item of the collection. If a match occurs, then the index of item is returned. If the middle item is greater than the item, then the item is searched in the sub-array to the left of the middle item. Otherwise, the item is searched for in the sub-array to the right of the middle item. This process continues on the sub-array as well until the size of the subarray reduces to zero. 
* If we are cutting somthing of size n into half over and over again then it takes log<2>n times before we get down to 1.
* Runtime compexity: $O(log_{2}n)$

### Polynomial multipication:
* Naive: 
  * Idea: 
  For two polynomials of order n-1, say, 
  $\newline
  a(x) = a_{1}x^{n-1} + a_{2}x^{n-2} + ... + a_{0} 
  \newline and \newline
  b(x) = b_{1}x^{n-1} + b_{2}x^{n-2} + ... + b<0> 
  \newline$
  The product polynomial will be of order 2n-1, say, 
  $\newline
  c(x) = c_{2n-2}x^{2n-2} + c_{2n -1}x^{2n-1}+....+c_{0} 
  \newline where: \newline
  c_{2n-2} = a<_{n-1}b_{n-1} \newline
  c_{2n-3} = a_{n-1}b_{n-2} + a_{n-2}b_{n-1}
  \newline ... \newline
  c_{2} = a_{2}b_{0} + a_{1}b_{1} + a_{0}b_{2} \newline
  c_{1} = a_{1}b_{0} + a_{0}b_{1} \newline
  c_{0} = a_{0}b_{0} \newline$
  Use above idea using two iterative loop to calculate all the coefficients. Notice that coeffiecent $c_{k}$ is sum of all those $a_{i}b_{j}$ such that i+j = k. 
  * Runtime complexity: O(n^(2))
* Naive divide and conquer: 
  * Idea: 
  Consider two polnomials, 
  $\newline
  a(x) = a_{1}x^{n-1} + a_{2}x^{n-2} + ... + a_{0} 
  \newline and \newline
  b(x) = b_{1}x^{n-1} + b_{2}x^{n-2} + ... + b<0> 
  \newline$ 
  We could write,
  $\newline
  a(x) = d_{1}(x)x^{n/2} + d_{0}(x)b(x) = e_{1}(x)x^{n/2} + e_{0}(x) 
  \newline then \newline
  a(x)b(x) = (d_{1}e_{1})x^{n} + (d_{1}e_{0} + d_{0}e_{1})x^{n/2} + d_{0}e_{0} \newline$
  * Note: we could always pad the polynomial in a way that n is multiple of 2. 
  * Divide problem of size n into 4 subproblem of size n/2 using above idea and keep doing it recursively till its become subproblems of size 1.
  * Hence, we could write recursive realtion as
  $T(n) = 4T(n/2) + O(n)$ where $O(n)$ is time required to evaluate expression (apart from solving subproblems)
  * Runtime complexity: O(n^(log<2>4)) or O(n^2)
* Fast divide and conquer:
  * Idea: 
  $x = ac + ad + bc + bd$ involves 4 multiplications whereas same could be done with just 3 multiplication because $bc + bd = (a+b)(c+d) - ac - ad$
   * Divide problem into 3 sub-problem at each level using above concept
  * Hence, we could write recursive realtion as $T(n) = 3T(n/2) + O(n)$ where $O(n)$ is time required to evaluate expression (apart from solving subproblems)
  * Runtime complexity: $O(n^{log_{2}3)})$ or $O(n^{1.59})$ which significant reduction in runtime complexcity in compare to naive divide-and-conquer because of recursive application of small trick mentioned above
  * Note: Idea of polynomial multipication could be easily applied to multiplication of two n digit numbers. For two n digit numbers $\newline a = a_{1}a_{2}...a_{n} 
  \newline and \newline 
  b = b_{1}b_{2}...b_{n} \newline$
  create two polynomials 
  $\newline 
  a(x) = a_{1}x^{n-1} + a_{2}x^{n-2} + ... + a_{n} 
  \newline and \newline 
  b(x) b_{1}x^{n-1} + b_{2}x^{n-2} + ... + b_{n} \newline$ 
  respectively. Next, do polynomial multiplication $c(x) = a(x)b(x)$. For each coefficient of $c$ which is greated than 9, keep the digit at unit place and add 1 to the coefficient left to it. Now replace $x$ in $c(x)$ with 10 to get product of two digits.

### Sorting:
* Selection sort:
  * This sorting algorithm is an in-place comparison-based algorithm in which the list is divided into two parts, the sorted part at the left end and the unsorted part at the right end. 
  * Initially, the sorted part is empty and the unsorted part is the entire list.The smallest element is selected from the unsorted array and swapped with the leftmost element, and that element becomes a part of the sorted array. This process continues moving unsorted array boundary by one element to the right.
  * Runtime-complexity: O(n^2)

* Merge sort:
  * It uses divide-and-conquer algorithm startegy to solve sorting problem. It recursively divides the array into equal halves, sort them and then combines them in a sorted manner till subproblem size is one. For combinig, it simply checks first element of the sorted array and move the one which is smaller to a the array storing combined array till both  sorted array reduce to size 0.
  * Runtime complexity:
    * Recursive relation: 
    $\newline T(n) = 2T(n/2) + O(n) \newline$
    where $0(n)$ is time combine the solved subproblems
    * Using master theorm runtime complexity of merge sort could be given by $O(n(log(n)))$
    * Any comparison based sorting algorithm will have runtime complexity of >= O(nlog(n)) in worst case which means merge sort is asymptotically optimal but note that extra time and space which goes in moving the data to new merged array.
    
* Counting sort: 
  * Sorting without comparison if we know the range of element in integer array then scan through array and count the occurence of each element then create sorted array based  on the count.
  * Runtime complexity: $O(n+m)$ where n is number of elelment in array and m is size of the range of the element.

* Randomized quick sort:
  * Comparison based algorithm 
  * Strategy: Generate an index between lower and upper bound of array and swap first element of array with the element at generated random index. Take first element of of array $A$, call it pivot $x = A[l]$ Then move $i$ on $l+1$ to $r$ (the end of the array) maintaining following invariant:
  $\newline 
  A[k] <= x \;for \;all\; l+1 <= k <=j_{1}
  \newline
  A[k] = x \;for \;all\; j_{1}+1 <= k <= j_{2}
  \newline 
  A[k] >= x \;for \;all\; j_{2}+1 <= k <= r \newline$
  you can do this by starting with $j = l$ and as you increment $i$, incrementing $j$ by 1 followed by swapping $A[j]$ with $A[i]$ when you  encounter $A[i] > x$. At the end move $A[l]$ to its final place by swapping $A[l]$ and $A[j]$. Do it recursively to sort the complete array
  * Runtime complexity: $O(nlog(n))$ (on average, while worst case runtime is o(n^2))
  * Space complexity: In general: $O(n)$ but could be reduced to: $O(log(n))$

### Reading resources
* Sanjoy Dasgupta, Christos Papadimitriou, and Umesh Vazirani. Algorithms (1st Edition). McGraw-Hill Higher Education. 2008.
  * Polynomial multiplication: Section 2.1
  * Master Theorem: Section 2.2
  * Merge sort and lower bound for comparison based sorting: Section 2.3
* Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, Clifford Stein. Introduction to Algorithms (3rd Edition). MIT Press and McGraw-Hill. 2009.
  * Quick sort: Chapter 7
