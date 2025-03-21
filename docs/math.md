# Math

## Get digits of a number

=== "Intuition"

    1. Use modulo 10 to extract last digit
    2. Update `n` by subtracting last digit
    3. Divide `n` by 10 (shifts penultimate digit to last)
    4. Repeat until `n` = 0

=== "Algorithm"

    ``` python
    n = 123
    digits = []
    while True:
        remainder = n % 10
        digits.append(remainder)
        n -= remainder
        if n == 0:
            break
        n = n // 10
    # digits: [1, 2, 3]
    ```

## Check if a Palindrome

=== "Intuition"

    !!! note Definition
        An integer is a palindrome when it reads the same forward and backward.
    
    
    Intuition is based on getting the digits of a number. Albeit one could also use string representation of a number.

    1. Use modulo 10 to extract last digit. Add to `reverse` (initially 0)
    2. Update `n` by subtracting last digit
    3. Divide `n` by 10 (shifts penultimate digit to last), multiply `reverse` by 10.
    4. Repeat until `n` = 0
    5. If reverse equal original n then n is palindrome.

=== "Algorithm"

    ``` python
    def isPalindrome(x: int) -> bool:
        if x < 0:
            return False
        n = x
        reverse = 0
        while x > 0:
            remainder = x % 10
            reverse = (reverse * 10) + remainder
            x = x // 10
        return n == reverse
    ```

## Happy Number


=== "Intuition"

    A happy number is a number defined by the following process:

    * Starting with any positive integer, replace the number by the sum of the squares of its digits.
    * Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
    * Those numbers for which this process ends in 1 are happy.

=== "Algorithm"

    ``` python
    def isHappy(n: int) -> bool:
        if n < 0:
            return False
        previous = []
        while True:
            val = n
            digits = []
            while True:
                remainder = val % 10
                digits.append(remainder ** 2)
                val -= remainder
                if val == 0:
                    break
                val = val // 10
            n = sum(digits)
            if n == 1:
                return True
            elif n in previous:
                return False
            previous.append(n)
        return False
    ```
