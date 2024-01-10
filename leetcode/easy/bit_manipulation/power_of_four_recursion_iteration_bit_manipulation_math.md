# 1/9/2024

## [🏠 Back to Home](https://dev-tae.github.io)

## [Power of Four](https://leetcode.com/problems/power-of-four/description/) (Link to Leetcode)

# Intuition
To determine if a number is a power of 4, we want to keep dividing the number until it reaches 1, since 4^0 is 1. This implies that the problem can be solved using either recursion or a loop, as we have a clear base case.


# Approach 1: Recursion
Our primary base case is when the leftover value of a number is 1. If this is the case, we return True.
```
if n == 1:
   return True
```
Now, we'll add a few more conditions. If the remainder of n divided by 4 is 0 (n % 4 == 0), then we recursively call the function until we reach the base case. If the remainder is not 0, then we return False.

```
if n % 4 == 0:
   return self.isPowerOfFour(n // 4)
# If remainder is not 0, it is not a power of four.
return False
```

However, if we run the code we have so far, we'll encounter a `RecursionError: maximum recursion depth exceeded`. This happens because we missed an edge case: a number becomes 0 if we keep dividing by 4, as the remainder never reaches 0. To handle this, we need another base case: return False if n becomes 0.
```
if n == 0:
   return False
```

# Complexity
- Time complexity: O(log N)
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity: O(log N)
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
class Solution:
    def isPowerOfFour(self, n: int) -> bool:
        if n == 0:
            return False
        if n == 1:
            return True
        if n % 4 == 0:
            return self.isPowerOfFour(n // 4)
        return False
```

# Approach 2: Iteration
The iterative approach is more straightforward and requires less code. We can simply use a while loop that continues until the number is reduced to 1 or 0. It's important to note that we use floating-point division here to get the correct output.
```
while n > 1:
   n /= 4
```
If n is 1, then it is a power of four; otherwise, it is not.
```
return n == 1
```


# Complexity

- Time complexity: O(log N)
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity: O(1)
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
class Solution:
    def isPowerOfFour(self, n: int) -> bool:
        while n > 1:
            n /= 4
        return n == 1
```

# Approach 3: Math
To determine if a number `n` is a power of four, we can use a mathematical approach. For `n` to be a power of four, it must satisfy the equation `n = 4^x` for some integer `x`. This can be rewritten in logarithmic form as `x = log4(n)`. We can check if `n` is indeed a power of four by verifying if `x` is an integer.

In Python, we do this by comparing the logarithmic result to its integer part using `int(log_n)`:

```
log_n = math.log(n, 4)
return log_n == int(log_n)
```

We also need a base case for when the value is less than or equal to 0. We return False in this case. The reason for including the less than condition is that we can't take the logarithm of negative numbers, as it would throw a math domain error:
```
if n <= 0:
   return False
```

# Complexity

- Time complexity: O(1)
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity: O(1)
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
class Solution:
    def isPowerOfFour(self, n: int) -> bool:
        if n <= 0:
           return False
        log_n = math.log(n, 4)
        return log_n == int(log_n)
```
# Approach 4: Bit Manipulation