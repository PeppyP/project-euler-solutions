## Problem 1 

**Pierre Sejourne** - C++  
The sum of all natural numbers up to n is given by $\frac{x * (x + 1)}{2}\$. This is clearly faster than looping each integer between 1 and 1000.  
However, we're looking for the sum of a subset of those numbers, specifically every 3rd and 5th. This can be done by substituting $x$ for $\frac{x}{n}\$, then multiplying the result by $n$, where $n$ is the factor of the subset we want.  
For mathematical justification of this, call the triangular sum $f(x)$. Dividing the input reduces the range of $f(x)$, then scaling the function effectively converts the range from sequential integers to multiples of $n$. So, for $f(9)$, the function effectively sums the set {1, 2, 3, 4, 5, 6, 7, 8, 9}, for $f(\frac{9}{3}\)$, the function sums {1, 2, 3}. Multiplying $1 + 2 +3$ by 3 gives you {3, 6, 9}, the set that we want.   
However, if we just sum every 3rd number and every 5th number, multiples of 15 will be counted twice, since $15 = 3 * 5$. Solving this is as easy as considering every 15th number and subtracting that from the total.  
This could easily be made into a function, but I felt it unnecessary given the lack of variation in the problem and how it would only have 3 calls. It would make it look cleaner but wouldn't simplify anything.
```C++
unsigned long long n;
std::cin >> n;
n--;
std::cout << ( 3*((n/3)*(n/3 + 1)/2) + 5*((n/5)*(n/5 + 1)/2) - 15*((n/15)*(n/15 + 1)/2) ) << std::endl;
```
**Lachlan Xiu** - Python  
Up to 1000 means I can do a loop of every number quickly. One-line solution.
```python
print(str(sum(x for x in range(1, 1000, 1) if (x%3 == 0 or x%5 == 0))))
```
---
## Problem 2

**Pierre Sejourne** - C++  
  
---
## Problem 3

**Pierre Sejourne** - C++  
  
---
## Problem 4

**Pierre Sejourne** - C++  
  
---
## Problem 5

**Pierre Sejourne** - Maths&Logic  
  
---
