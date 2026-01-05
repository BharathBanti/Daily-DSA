## LeetCode #509 — Fibonacci Number

---

### 1️⃣ Problem Statement

**LeetCode Link:** [Fibonacci Number (LC #509)](https://leetcode.com/problems/fibonacci-number/)

The Fibonacci numbers, commonly denoted as `F(n)`, form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is:

F(0) = 0, F(1) = 1
F(n) = F(n-1) + F(n-2), for n > 1

ruby
Copy code

Given `n`, return the `nᵗʰ` Fibonacci number.

**Examples:**

Example 1:
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1

Example 2:
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2

Example 3:
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3

yaml
Copy code

**Constraints:**  
- `0 <= n <= 30`  

---

### 2️⃣ Approach and Logic 💡

- ✅ Base cases: F(0) = 0, F(1) = 1  
- ✅ Use **iteration** instead of recursion to avoid repeated calculations (Recursion → exponential time)  
- ✅ Maintain two variables to store previous two Fibonacci numbers  
- ✅ Update iteratively until reaching `n`  

**Why iteration?**  
- Recursive approach recomputes the same Fibonacci numbers multiple times → inefficient  
- Iterative approach is **O(n) time** and **O(1) space**  

---

### 3️⃣ Visualization 🔍

Example: `n = 5`  

| Step | prev1 | prev2 | Current F(n) |
|------|-------|-------|---------------|
| Init | 0     | 1     | -             |
| 1    | 0     | 1     | 1             |
| 2    | 1     | 1     | 2             |
| 3    | 1     | 2     | 3             |
| 4    | 2     | 3     | 5             |

Result: F(5) = 5 ✅

---

### 4️⃣ Dry Run 🏃

Input: `n = 6`

| Step | prev1 | prev2 | Current F(n) |
|------|-------|-------|---------------|
| 0    | 0     | 1     | -             |
| 1    | 1     | 1     | 1             |
| 2    | 1     | 2     | 2             |
| 3    | 2     | 3     | 3             |
| 4    | 3     | 5     | 5             |
| 5    | 5     | 8     | 8             |

Output: `8`

---

### 5️⃣ Edge Cases ⚠️

- n = 0 → return 0  
- n = 1 → return 1  
- Maximum n = 30 → iterative approach handles easily  
- Avoid recursion for larger `n` to prevent stack overflow  

---

### 6️⃣ Java Code 🟦

```java
class Solution {
    public int fib(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;

        int prev1 = 0, prev2 = 1;
        for (int i = 2; i <= n; i++) {
            int current = prev1 + prev2;
            prev1 = prev2;
            prev2 = current;
        }

        return prev2;
    }
}
```
---
## 7️⃣ JavaScript Code 🟨
```javascript
function fib(n) {
    if (n === 0) return 0;
    if (n === 1) return 1;

    let prev1 = 0, prev2 = 1;
    for (let i = 2; i <= n; i++) {
        let current = prev1 + prev2;
        prev1 = prev2;
        prev2 = current;
    }

    return prev2;
}

// Examples
console.log(fib(2)); // 1
console.log(fib(3)); // 2
console.log(fib(4)); // 3
console.log(fib(6)); // 8
```
---

## 8️⃣ Time and Space Complexity ⏱️
- Time Complexity: O(n)

Reason: We compute Fibonacci numbers from 2 to n iteratively

- Space Complexity: O(1)

Reason: Only two variables are maintained, no extra data structures

## 9️⃣ Interview Traps ⚠️
- Using recursion for larger n → exponential time ❌

- Forgetting base cases F(0) and F(1) ❌

- Using extra arrays unnecessarily → wastes space ❌

- Confusing prev1 and prev2 updates in iteration ❌
