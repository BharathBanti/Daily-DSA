## LeetCode #9 — Palindrome Number

---

### 1️⃣ Problem Statement

**LeetCode Link:** [Palindrome Number (LC #9)](https://leetcode.com/problems/palindrome-number/)

Given an integer `x`, return `true` if `x` is a **palindrome**.  
An integer is a palindrome when it reads the same backward as forward.  

**Description:**  
- A palindrome number is a number that remains the same when its digits are reversed.  
- You **cannot** convert the number to a string.  

**Examples:**

Example 1:
Input: x = 121
Output: true
Explanation: 121 reads the same backward and forward.

Example 2:
Input: x = -121
Output: false
Explanation: -121 reads 121- backward which is different.

Example 3:
Input: x = 10
Output: false
Explanation: 10 reads 01 backward, which is not the same as 10.


**Constraints:**  
- `-2^31 <= x <= 2^31 - 1`  

---

### 2️⃣ Approach and Logic 💡

- ❌ Negative numbers are **never palindromes**  
- ❌ Numbers ending with 0 (except 0 itself) cannot be palindromes  
- ✅ Reverse **only half** of the number and compare with the other half  
- ✅ For numbers with **odd digits**, ignore the middle digit when comparing  

**Why half-reversal?**  
- Reversing the entire number can cause **integer overflow**  
- Reversing only half reduces unnecessary operations and space usage  

---

### 3️⃣ Visualization 🔍

Example: `x = 1221`

| Original x | Step       | Reversed Half |
|------------|------------|---------------|
| 1221       | Initial    | 0             |
| 1221       | Iteration1 | 1             |
| 122        | Iteration2 | 12            |
| 12         | Stop       | 12            |

Compare: `x == reversedHalf → true ✅`

---

### 4️⃣ Dry Run 🏃

Input: `x = 12321`

| Step | x     | Reversed Half | Explanation                        |
|------|-------|---------------|------------------------------------|
| 1    | 12321 | 0             | Initial state                      |
| 2    | 1232  | 1             | reversedHalf = 0*10 + 12321%10    |
| 3    | 123   | 12            | reversedHalf = 1*10 + 1232%10     |
| 4    | 12    | 123           | reversedHalf = 12*10 + 123%10     |
| 5    | 12    | 123           | Stop, reversedHalf >= x, compare   |

Check: `x == Math.floor(reversedHalf / 10) → 12 == 12 ✅`  
Output: `true`

---

### 5️⃣ Edge Cases ⚠️

- Negative numbers → `-121` → `false`  
- Numbers ending with 0 → `10` → `false`  
- Single-digit numbers → always palindrome  
- Very large numbers → use half-reversal to avoid overflow  

---

### 6️⃣ Java Code 🟦

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0 || (x % 10 == 0 && x != 0)) return false;

        int reversedHalf = 0;
        while (x > reversedHalf) {
            reversedHalf = reversedHalf * 10 + x % 10;
            x /= 10;
        }

        return x == reversedHalf || x == reversedHalf / 10;
    }
}
```
### 7️⃣ JavaScript Code 🟨

```javascript
function isPalindrome(x) {
    if (x < 0 || (x % 10 === 0 && x !== 0)) return false;

    let reversedHalf = 0;
    while (x > reversedHalf) {
        reversedHalf = reversedHalf * 10 + x % 10;
        x = Math.floor(x / 10);
    }

    return x === reversedHalf || x === Math.floor(reversedHalf / 10);
}

// Examples
console.log(isPalindrome(121));   // true
console.log(isPalindrome(-121));  // false
console.log(isPalindrome(10));    // false
```

## 8️⃣ Time and Space Complexity ⏱️
Time Complexity: O(log10(n))

Reason: We only reverse half of the digits. Each iteration removes one digit from x.

Space Complexity: O(1)

Reason: Only a few variables used, no extra data structures.

## 9️⃣ Interview Traps ⚠️
- Forgetting negative numbers are never palindromes ❌

- Ignoring numbers ending with 0 (except 0 itself) ❌

- Reversing the entire number (risk of integer overflow in Java) ❌

- Not handling odd digit numbers correctly ❌
