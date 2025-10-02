+++
title = 'atoi()'
description = "LC8 took all of my time today. Pseudocoding here for reference later."
date = 2025-03-27
+++

[LC8](https://leetcode.com/problems/string-to-integer-atoi/) took all of my time today. Pseudocoding here for reference later --

### Problem Statement
Convert a string to integer - 
1. Leading whitespaces to be ignored
2. `+` or `-` to be taken into account for the integer sign
3. Non-digit characters to be ignored
4. Digit characters to be converted to integers
5. Constraint specifies a string length of 0 to 200, integer overflow is possible; answer in that case to be rounded off to the max/min integer value
6. Return the final signed integer

### Pseudocode
```sh
index = 0
answer = 0
sign = 1

if string length = 0, return 0

while (index < string.length AND leading whitespaces) {
    increment index
}

if (index < string.length AND current character + or -) {
    sign = 1 if '+' 
    OR
    sign = -1 if '-'
    increment index
}

while (index < string.length) {
    digit = (int) current character  ----- [- '0' in Java (some ASCII math)]
    if digit does not lie between 0 and 9, break loop

    check for integer overflow
        - MAX_INT / 10 > answer OR
        - MAX_INT / 10 == answer then last digit of MAX_INT to be less than current digit
    if integer overflow - return MAX or MIN int (check with sign)
    else add digit to answer
}

return answer

```
