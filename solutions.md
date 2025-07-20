## Problem 1 

**Pierre Sejourne** - C++    
The sum of all natural numbers up to x is given by $\frac{x * (x + 1)}{2}\$. This is faster than looping through each integer between 1 and 1000.  
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
There are many ways to find prime numbers, and I contemplated "use OEIS" here as a joke. Sadly, I doubt my humor would be appreciated.  
Anyway, I decided to implement a sieve of Eratosthenes since I was the first thing I thought of. This algorithm "finds" primes by sequentially disqualifying all non-prime numbers.  
Each number is represented by a boolean in an array that shows whether that number is prime. The array is initalised as all true, except for 0 and 1, and every even number greater than 2.  
Then, for each prime element, disqualify all multiples of it as they have that prime as a factor. You are left with an array where the nth element tells you if n is prime or not. You can then search for the 10,001th true in the array. Thanks to the [prime-counting function](https://www.mdpi.com/2227-7390/12/17/2624), we can know that 10001th prime will be roughly within the first 150,000 natural numbers, so that will be the size of our sieve. 
```C++
const int limit = 150000;
bool sieve[limit] = {};
for (int i = 3; i < limit; i += 2) {
  sieve[i] = true;
}
sieve[2] = true;
for (int i = 3; i * i < limit; i++) {
  if (sieve[i]) {
    for (int j = i * i; j < limit; j += i) {
      sieve[j] = false;
    }
  }
}
int count = 1;
for (int i = 3; i < limit; i += 2) {
  if (sieve[i]) {
    count++;
    if (count == 10001) {
      std::cout << i << std::endl;
      break;
    }
  }
}
```
---
## Problem 8

**Pierre Sejourne** - C++    
One thing to note is that as we move the 'head', the 13 digits that we are multiplying, along the string, the product is effectively divided by the previous digit and scaled by the next digit.  
So, to find the highest product we can just ignore any sequences that have a last digit that is lower than or equal to the next digit. Otherwise, we can multiply the digits and keep the highest of those multiples. This will take 1000 - 13 multiplications minus how many are removed from consideration by the greedy process.
```C++
long long productOfDigits(const string& digits, int start) {
    long long product = 1;
    for (int i = start; i < start + 13; i++) {
        if (digits[i] == '0') {
          return 0;
        }
        product *= digits[i] - '0';
    }
    return product;
}

string raw = "73167176531330624919225119674426574742355349194934...[The string]";
while (i + 13 <= raw.size()) {
  if (i + 13 < raw.size() && raw[i + 13] >= raw[i + 12]) {
    i++;
    continue;
  }

  long long currentProduct = productOfDigits(raw, i);
  if (currentProduct > maxProduct) {
    maxProduct = currentProduct;
  }

  i++;
}

std::cout << maxProduct << std::endl;
```
---
## Problem 9

**Pierre Sejourne** - C++    
The values for a, b, c need to fulfill the following criteria: $a^2 + b^2 = c^2$ and $a + b + c = 1000$. We can use this to weed out $a < 333$ and $b < 500$.
This leaves us with 111555 calculations (Sum of first 333 terms of $u<sub>1</sub> = 166, d = 1$), which is fast enough to compute within a reasonable amount of time, 1.37 seconds for me.  
There are of course better methods for finding Pythagorian triples, such as the sets of solutions given by Euclid's formula.  
```C++
int a, b, c;
for (a = 1; a < 333; a++) {
  for (b = a + 1; b < 500; b++) {
    c = 1000 - a - b;
    if (a*a + b*b == c*c) {
      std::cout << a * b * c << std::endl;
      return 0;
    }
  }
}
```
---
## Problem 10

**Pierre Sejourne** - C++    
Another problem that involves running through all of the prime numbers. This one will be done with the same algorithm as **Problem 7**, the Sieve of Eratosthenes.  
Once it generates all of the primes up to 2 million, we can just scan through the array and sum the indexes of all the prime numbers. Note that the sum starts at 2 and ignores even numbers since 2 is the only even prime.
```C++
const int limit = 2000000;
bool sieve[limit] = {};
for (int i = 3; i < limit; i += 2) {
  sieve[i] = true;
}
sieve[2] = true;
for (int i = 3; i * i < limit; i += 2) {
  if (sieve[i]) {
    for (int j = i * i; j < limit; j += i) {
      sieve[j] = false;
    }
  }
}
int sum = 2;
for (int i = 3; i < limit; i += 2) {
  if (sieve[i]) {
    sum += i;
  }
}
std::cout << sum << std::endl;
```
---
## Problem 11

**Pierre Sejourne** - C++  
The concepts of 'Right' and 'Left', 'Up' and 'Down' are equivalent in this problem. So, we can just preform 4 iterations over each cell to check for a valid 4-element segment in each of the 4 directions. If it’s within the grid bounds, we compute the product. If the product is larger than the previous maximum, we update the maximum. This takes 1600 iterations, of which ~1000 are valid. So, 3000 two-digit multiplications are done, which is viable for computers to do within a reasonable time.
```C++
std::vector<std::vector<int>> grid = {
  {8,2,22,97,38,15,0,40,0,75,4,5,7,78,52,12,50,77,91,8},
  {49,49,99,40,17,81,18,57,60,87,17,40,98,43,69,48,4,56,62,0},
  /*...[The entire 20x20 grid in this form]*/
};
long long maxProduct = 0;
for (int i = 0; i < 20; ++i) {
  for (int j = 0; j < 20; ++j) {
    if (j <= 16) {
      long long prod = 1;
      for (int k = 0; k < 4; k++) {
        prod *= grid[i][j + k];
      }
      maxProduct = std::max(maxProduct, prod);
    }
    if (i <= 16) {
      long long prod = 1;
      for (int k = 0; k < 4; k++) {
        prod *= grid[i + k][j];
      }
      maxProduct = std::max(maxProduct, prod);
    }
    if (i <= 16 && j <= 16) {
        long long prod = 1;
        for (int k = 0; k < 4; k++) {
          prod *= grid[i + k][j + k];
        }
      maxProduct = std::max(maxProduct, prod);
    }
    if (i <= 16 && j >= 3) {
      long long prod = 1;
      for (int k = 0; k < 4; k++) {
        prod *= grid[i + k][j - k];
      }
      maxProduct = std::max(maxProduct, prod);
    }
  }
}
std::cout <<  maxProduct << std::endl;
```
---
## Problem 12

**Pierre Sejourne** - C++  
The trick lies in efficiently calculating the number of divisors of a number. We do this by prime factorization: if $n = p_1^{a_1}\cdot p_2^{a_2}\cdot ...\cdot p_k^{a_k}$.  
Then the total number of divisors is given by $(a_1 + 1)(a_2 + 1)...(a_k + 1)$.  
To keep things fast, we precompute primes using a sieve and apply this formula to each triangle number. Since each triangle number is a product of $n$ and $n + 1$ (divided by 2), we take advantage of the fact that n and $n + 1$ are coprime, which means we can factor them separately and multiply the result.
```C++
std::vector<int> generatePrimes(int max) {
  std::vector<bool> isPrime(max + 1, true);
  std::vector<int> primes;
  isPrime[0] = isPrime[1] = false;
  for (int i = 2; i <= max; ++i) {
    if (isPrime[i]) {
      primes.push_back(i);
      for (int j = i * i; j <= max; j += i) {
        isPrime[j] = false;
      }
    }
  }
  return primes;
}

int countDivisors(int n, const std::vector<int>& primes) {
  int total = 1;
  int remaining = n;
  for (int p : primes) {
    if (p * p > remaining) {
      break;
    }
    int count = 0;
    while (remaining % p == 0) {
      remaining /= p;
      count++;
    }
    if (count > 0) {
    total *= (count + 1);
    }
  }
  if (remaining > 1) {
    total *= 2;
  }
  return total;
}

std::vector<int> primes = generatePrimes(1000);
int n = 1;
while (true) {
  int a = n;
  int b = n + 1;
  if (a%2 == 0) {
    a /= 2;
  } else {
    b /= 2;
  }
  int divA = countDivisors(a, primes);
  int divB = countDivisors(b, primes);
  if (divA * divB > 500) {
    long long triangle = 1LL * n * (n+1)/2;
    std::cout << triangle << std::endl;
    break;
  }
  n++;
}
return 0;
```
---
## Problem 13

**Pierre Sejourne** - C++  
To determine the first 10 digits of a sum, we don’t need the full precision of the sum, only enough to ensure that rounding the discarded digits doesn't affect the top 10.  
A sum of 100 50-digit numbers could have up to 52 digits (in the 'worst' case). So the first 10 digits can only be affected by the first 13 digits of each number. Therefore, we can safely truncate each number to its first 13 digits, sum them as long long, and extract the first 10 digits of the result.
```C++
std::string numbers_raw = "37107287533902102798797998220837590246510135740250\n...[The string of all the numbers separated by a newline]";
std::stringstream ss(numbers_raw);
std::string line;
long double total = 0;
while (getline(ss, line)) {
  std::string prefix = line.substr(0, 13);
  total += stold(prefix); 
}
std::string result = std::to_string((long long)total);
std::cout << result.substr(0, 10) << std::endl;
return 0;
```
---
## Problem 14

**Pierre Sejourne** - C++  
The [Collatz conjecture](https://en.wikipedia.org/wiki/Collatz_conjecture) is a well-studied mathematics theorem that asks if a recursive sequence terminates for any starting value. So far, all starting values have been found to terminate after some number of terms.
We can compute the number of terms in a given Collatz sequence fairly easily, though repeatedly calculating the entire chain for long starting values takes time. To improve performance, the program stores the sequence lengths of previously computed values in a vector. This reduces the number of repeated calculations dramatically, particularly for values that appear in multiple sequences. 
A recursive function computes and memoizes sequence lengths for numbers under one million. For values larger than that it computes them on the fly but does not store them. Then we can check each starting value and record the one that generates the longest sequence.
```C++
long long collatzLength(long long n, std::vector<int>& cache) {
  if (n < 1000000 && cache[n] != 0) {
    return cache[n];
  }
  long long next;
  if (n % 2 == 0)
    next = n / 2;
  else {
    next = 3 * n + 1;
  }
  long long length = 1 + collatzLength(next, cache);
  if (n < 1000000) {
    cache[n] = length;
  }
  return length;
}

std::vector<int> cache(1000000, 0);
cache[1] = 1;
int maxStart = 1;
int maxLength = 1;
for (int i = 2; i < 1000000; i++) {
  int len = collatzLength(i, cache);
  if (len > maxLength) {
    maxLength = len;
    maxStart = i;
  }
}
std::cout << maxStart << std::endl;
```
---
## Problem 15

**Pierre Sejourne** - Maths & Logic  
This is a classic combinatorics problem. Each path consists of exactly 20 right moves and 20 down moves, in some order.  
Therefore, every valid path is simply a permutation of these 40 moves where the order of moves matters, but the type of move is limited to 2 kinds.  
So, the number of such sequences is given by the binomial coefficient: $\binom{40}{20} = \frac{40!}{20!\cdot 20!} = \frac{40\cdot 39\cdot 38 \cdot 37\cdot ...\cdot 21}{20!}$.  
This gives us the answer.

---
## Problem 16

**Pierre Sejourne** - C++  
$2^{100}$ is a 31-digit integer, too large for native C++ types. But it’s also tame in structure as it's just a power of 2. So, we can use digit-wise arithmetic to simulate it instead.  
We represent the number as a vector<int> where each element is a digit. We start with 1, and multiply the number by 2, one digit at a time, 100 times. Then sum the elements of the vector.
```C++
void multiplyBy2(std::vector<int>& digits) {
  int carry = 0;
  for (size_t i = 0; i < digits.size(); i++) {
    int product = digits[i] * 2 + carry;
    digits[i] = product%10;
    carry = product / 10;
  }
  while (carry > 0) {
    digits.push_back(carry%10);
    carry /= 10;
  }
}

std::vector<int> digits = {1};
for (int i = 1; i <= 1000; i++) {
  multiplyBy2(digits);
}
int sum = 0;
for (int digit : digits) {
  sum += digit;
}
std::cout << sum << std::endl;
```
---
## Problem 17

**Pierre Sejourne** - C++  
This is doable on a per-case basis, but to do this efficiently, we can exploit the structure of the English number system's few base components: "one" to "nine", "eleven" to "nineteen", "twenty", "thirty", ..., "ninety", "hundred", "and", and "thousand".  
By decomposing each number into its components, and precomputing the letter counts for each component, we can reuse these values and efficiently build the total.
```C++
const int ones[] = { 0, 3, 3, 5, 4, 4, 3, 5, 5, 4, 3, 6, 6, 8, 8, 7, 7, 9, 8, 8 };
const int tens[] = { 0, 0, 6, 6, 5, 5, 5, 7, 6, 6 };

int numberLetterCount(int n) {
  if (n == 1000) {
    return 11;
  }
  int total = 0;
  int hundreds = n / 100;
  int remainder = n % 100;
  if (hundreds) {
    total += ones[hundreds] + 7; 
    if (remainder) {
      total += 3; 
    }
  }
  if (remainder >= 20) {
    total += tens[remainder / 10];
    total += ones[remainder % 10];
  } else if (remainder >= 1) {
    total += ones[remainder];
  }
  return total;
}

int sum = 0;
for (int i = 1; i <= 1000; ++i) {
  sum += numberLetterCount(i);
}
std::cout <<  sum << std::endl;
```
---
## Problem 18

**Pierre Sejourne** - C++  
This is a fairly standard dynamic programming problem, the thing to note is that the limited number of options allows you to simplify the calculation of later steps by substituting values that have already been found during computation. This allows us to just go through every possiblity from the bottom up, since the maximum from any starting position will either already be calculated or be the highest from among two values. So the calculations are just n comparisions, which is very easy for computers to do.  
The is no reason to do this for the small triangle in this problem, but **Problem 67** is a scaled version of this problem that requires a more efficient program.  
The rest of the program relates to flattening the triangle into a computer-readable format.
```C++
std::vector<std::vector<int>> parseTriangle(const std::string& data) {
  std::vector<std::vector<int>> triangle;
  std::istringstream iss(data);
  int value, row = 1;
  while (!iss.eof()) {
    std::vector<int> currentRow;
    for (int i = 0; i < row && iss >> value; i++) {
        currentRow.push_back(value);
    }
    triangle.push_back(currentRow);
    row++;
  }
  return triangle;
}

int maximumPathSum(std::vector<std::vector<int>>& triangle) {
  for (int row = triangle.size() - 2; row >= 0; row--) {
    for (size_t col = 0; col < triangle[row].size(); col++) {
      triangle[row][col] += std::max(triangle[row + 1][col], triangle[row + 1][col + 1]);
    }
  }
  return triangle[0][0];
}

std::string triangleData = "75 95 64 17 47 82...[Each number in the triangle separated by a space]";
std::vector<std::vector<int>> triangle = parseTriangle(triangleData);
int maxTotal = maximumPathSum(triangle);
std::cout << maxTotal << std::endl;
```
---
## Problem 19

**Pierre Sejourne** - C++  
The first problem directly involving modular arithmetic, if CodeForces[<sup>[1]</sup>](#1) has taught me anything, then it'll keep appearing ad nauseam. The days of the week repeat every 7 days, so we can track the day of the week using modulo 7 arithmetic.  
We define: 0 = Sunday, 1 = Monday, ..., 6 = Saturday. Each month advances the weekday by (number of days in the month) % 7. This gives a modular recurrence. If the 1st of a month is Tuesday, and the month has 31 days, the next 1st will fall on (2 + 31) mod 7 = 5. We simulate this process over the given period, checking if a month begins on a Sunday, and count each case.   
To determine month lengths, we can just copy the giving rules and check for year divisibility for February.  
```C++
bool isLeapYear(int year) {
  if (year % 4 != 0) {
    return false;
  }
  if (year % 100 == 0 && year % 400 != 0) {
    return false;
  }
  return true;
}

int monthDays[] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
int dayOfWeek = 1; 
int count = 0;
for (int year = 1900; year <= 2000; year++) {
  for (int month = 0; month < 12; month++) {
    if (year >= 1901 && dayOfWeek == 0) {
      count++;
    }
    int daysThisMonth = monthDays[month];
    if (month == 1 && isLeapYear(year)) {
      daysThisMonth++;
    }
    dayOfWeek = (dayOfWeek + daysThisMonth) % 7;
  }
}
std::cout << count << std::endl;
```
---
## Problem 20

**Pierre Sejourne** - C++  
Factorials grow very fast, too fast to be easily stored in native c++ types.  
So, we instead store $100!$ in a vector\<int\> as each digit of the result. Each multiplication step behaves like a convolution of a number with a digit array, and carries are propagated just like in arithmetic.  
```C++
void multiply(std::vector<int>& digits, int x) {
    int carry = 0;
    for (int& d : digits) {
        int product = d * x + carry;
        d = product % 10;
        carry = product / 10;
    }

    while (carry > 0) {
        digits.push_back(carry % 10);
        carry /= 10;
    }
}

std::vector<int> digits = {1};
for (int i = 2; i <= 100; i++) {
  multiply(digits, i);
}
int sum = 0;
for (int d : digits) {
  sum += d;
}
std::cout << sum << std::endl;
```
---
## Problem 21

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 22

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 23

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 24

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 25

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 26

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 27

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 28

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 29

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 30

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 31

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 32

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 33

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 34

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 35

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 36

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 37

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 38

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 39

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 40

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 41

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 42

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 43

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 44

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 45

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 46

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 47

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 48

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 49

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 50

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 51

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 52

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 53

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 54

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 55

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 56

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 57

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 58

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 59

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 60

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 61

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 62

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 63

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 64

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 65

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 66

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 67

**Pierre Sejourne** - Already Solved  
Exactly the same program and as **Problem 18**, but this time reading the string from a file instead of a literal because it's too long to type.  

---
## Problem 68

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 69

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 70

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 71

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 72

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 73

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 74

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 75

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 76

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 77

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 78

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 79

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 80

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 81

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 82

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 83

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 84

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 85

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 86

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 87

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 88

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 89

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 90

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 91

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 92

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 93

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 94

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 95

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 96

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 97

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 98

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 99

**Pierre Sejourne** - C++  

```C++

```
---
## Problem 100

**Pierre Sejourne** - C++  

```C++

```
---
<a id="1"></a>$^{[1]}$ Thank you to the glorious **MikeMirzayanov** for Polygon and this wonderful platform!
