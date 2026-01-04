# LeetCode #7 — Reverse Integer

**Difficulty:** Medium  
**Topic:** Math / Integer Manipulation  

---

## LeetCode 
LC#07 : https://leetcode.com/problems/reverse-integer/description/

## Problem Statement

Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.
Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

---

## Concept

At a glance, this problem looks like a basic digit reversal task.  
But the real difficulty is not reversing the number — it’s **handling overflow safely**.

The idea is to:
- Extract the last digit using modulo
- Build the reversed number step by step
- Ensure the value never crosses the 32-bit integer limit

Overflow must be checked **before** updating the result, not after.

---

## Visualization

Think of the number as digits being removed from right to left.

Example: `123`

Initial:
x = 123, result = 0

Step 1:
digit = 3
result = 0 * 10 + 3 = 3

Step 2:
digit = 2
result = 3 * 10 + 2 = 32

Step 3:
digit = 1
result = 32 * 10 + 1 = 321

yaml
Copy code

Each step grows the result by a factor of 10, which is why overflow becomes a risk.

---

## Dry Run

### Input
x = -123

shell
Copy code

### Execution
x = -123, result = 0
digit = -3 → result = -3

x = -12
digit = -2 → result = -32

x = -1
digit = -1 → result = -321

shell
Copy code

### Output
-321

yaml
Copy code

Negative values are handled naturally without any special logic.

---

## Edge Cases

1. **Overflow**
x = 1534236469

pgsql
Copy code
Reversed value exceeds 32-bit range → return `0`

2. **Trailing zeros**
x = 120 → 21

markdown
Copy code

3. **Single digit**
x = 7 → 7

markdown
Copy code

4. **Minimum integer**
x = -2147483648 → 0

yaml
Copy code

---

## Time & Space Complexity

- **Time Complexity:** `O(log₁₀(n))`  
  (Number of digits in the integer)

- **Space Complexity:** `O(1)`  
  (Constant extra space)

---

## Java Solution

```java
class Solution {
    public int reverse(int x) {
        int result = 0;
        while (x != 0) {
            int digit = x % 10;
            x /= 10;
            if (result > Integer.MAX_VALUE / 10 ||
               (result == Integer.MAX_VALUE / 10 && digit > 7)) {
                return 0;
            }

            if (result < Integer.MIN_VALUE / 10 ||
               (result == Integer.MIN_VALUE / 10 && digit < -8)) {
                return 0;
            }

            result = result * 10 + digit;
        }

        return result;
    }
}

````
---

## JavaScript Solution

```JavaScript
var reverse = function(x) {
    let result = 0;
    const INT_MAX = 2147483647;
    const INT_MIN = -2147483648;

    while (x !== 0) {
        let digit = x % 10;
        x = Math.trunc(x / 10);

        if (
            result > Math.trunc(INT_MAX / 10) ||
            (result === Math.trunc(INT_MAX / 10) && digit > 7)
        ) {
            return 0;
        }

        if (
            result < Math.trunc(INT_MIN / 10) ||
            (result === Math.trunc(INT_MIN / 10) && digit < -8)
        ) {
            return 0;
        }

        result = result * 10 + digit;
    }

    return result;
};
```
---
## Interview Traps

- Reversing using strings instead of math operations

- Forgetting to check overflow

- Checking overflow after updating the result

- Assuming negative numbers need special handling

Interviewers care more about safe arithmetic than shortcuts.
