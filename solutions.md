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
This problem requires us to consider every even Fibonacci number, so we will need to calculate every one, the most efficient way to do this is to simply iterate through every value by repeatedly adding variables to each other and adding to a sum when the head variable is even.  
There isn't much to say, its just a simple problem with an uncomplicated solution.  
```C++
unsigned long long n;
std::cin >> n;
unsigned long long sum = 0;
unsigned long long a = 1;
unsigned long long b = 2;
while (b <= n) {
  if (b%2 == 0) {
        sum += b;
  }
  unsigned long long c = a + b;
  a = b;
  b = c;
}
std::cout << sum << std::endl;
```
---
## Problem 3

**Pierre Sejourne** - C++  
To find the largest prime factor of a composite number x, we can divide x repeatedly, starting with a prime number, until you end up with another prime or exhaust all other options. The last value after the divisions end is the largest prime factor. This is because at every step, all smaller prime divisors are divided out.  
Since 2 is the only even prime number, we divide x by 2 repeatedly until it is no longer divisible, or until it becomes 2 itself. This removes all even factors.  
Once all factors of 2 are removed, any remaining factors must be odd. We loop through odd numbers only starting from 3, incrementing by 2, which skips all even composites.  
We only check factors up to $\sqrt{x}$ because if x has any factor greater than $\sqrt{x}$, it must also have a corresponding factor less than $\sqrt{x}$.  
Once we divide out all small prime factors, if any factor remains, it must itself be prime.  
```C++
unsigned long long n;
std::cin >> n;
while (n%2 == 0 && n != 2) {
  n /= 2;
}
for (unsigned long long factor = 3; factor * factor <= n; factor += 2) {
  while (n%factor == 0 && n != factor)
    n /= factor;
}
std::cout << n << std::endl;
```
---
## Problem 4

**Pierre Sejourne** - C++  
The questions asks for two three-digit numbers that form a palindrome. This means that we have to look through each combination of 100-999, determine whether it's a palindrome, then store the highest palindrome that we find.  
The second loop starts from the first factor since lower numbers would have already been tested, and ends when a palindrome is found. This is because we check the palindromes from descending factors as we're searching for the maximum, so any further tests will only yield lower numbers.
```C++
bool isPalindrome(int n) {
    int original = n;
    int reversed = 0;
    while (n > 0) {
        int digit = n % 10;
        reversed = reversed * 10 + digit;
        n /= 10;
    }
    return original == reversed;
}

int max = 0;
for (int i = 999; i >= 100; --i) {
  for (int j = i; j >= 100; --j) {
    if (i * j <= max) break;
    if (isPalindrome(i * j)) {
      max = i * j;
      break;
    }
  }
}
std::cout << max << std::endl;
```
---
## Problem 5

**Pierre Sejourne** - Maths & Logic  
The smallest number that has all of a set of numbers as factors is the Lowest Common Multiple (LCM) of those numbers.  
There are several ways to find an LCM, but the easiest is to multiply each unique prime factor among the numbers.  
The prime factors of 1-20 are $1, 2, 3, 2^2, 5, 2\cdot3, 7, 2^3, 3^2, 2\cdot5, 11, 2^2\cdot3, 13, 2\cdot7, 3\cdot5, 2^4, 17, 2\cdot3^2, 19, 2^2\cdot5$.  
The highest power of each factor among them are $1, 2^4, 3^2, 5, 7, 11, 13, 17, 19$.  
Multiplying them together gives the answer, $1\cdot2^4\cdot3^2\cdot5\cdot7\cdot11\cdot13\cdot17\cdot19$.  

---
## Problem 6

**Pierre Sejourne** - C++  
The sum of all natural numbers to x is given by $\frac{x * (x + 1)}{2}\$, squaring this gives us the square of the sum of all natural numbers up to x, $\frac{x^2 * (x + 1)^2}{4}\$.  
The sum of the squares of all natural numbers up to x is given by $\frac{x * (x + 1) * (2x + 1)}{6}\$.  
The difference between these sums is $\frac{x^2 * (x + 1)^2}{4}\ - \frac{x * (x + 1) * (2x + 1)}{6}\ = \frac{3x^4 + 6x^3 + 3x^2}{12}\ - \frac{4x^3 + 6x^2 + 2x}{12}\ = \frac{3x^4 + 2x^3 - 3x^2 - 2x}{12}\$.  
This value is what the problem is asking for, so that's all we need to do.
```C++
unsigned long long n;
std::cin >> n;
std::cout << ( 3*n*n*n*n + 2*n*n*n - 3*n*n - 2*n )/12 << std::endl;
```
---
## Problem 7

**Pierre Sejourne** - C++  

```C++

```
---
