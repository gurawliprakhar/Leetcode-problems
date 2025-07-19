

---

### 🎬 ** Split Array by Prime Indices | Leetcode Biweekly Contest 161 Q1**

---



---

#### 📄 **\[Problem Statement - ]**

```
🎤 "You are given an integer array called `nums`. We need to split this array into two new arrays — A and B — based on a simple rule:

- All elements at **prime indices** go into array A.
- All other elements go into array B.

Once split, we return the **absolute difference** between the sums of arrays A and B.

That is: return |sum(A) - sum(B)|"
```

---

#### 🧠 **\[Understanding with Example - ]**

```
🎤 "Let’s understand with an example:

Input: nums = [2, 3, 4]

The indices are: 0 → 2, 1 → 3, 2 → 4

Index 2 is prime → goes to A → A = [4]
Indices 0 and 1 are not prime → go to B → B = [2, 3]

Sum(A) = 4, Sum(B) = 5 → Output = |4 - 5| = 1"
```

---

#### 🔎 **\[Prime Index Logic ]**

```
🎤 "Now the main challenge is identifying whether an index is prime. Remember, a prime number is greater than 1 and only divisible by 1 and itself.

So we’ll write a helper function `isPrime(i)` to check if an index is prime."
```

---

#### 💻 **\[Java Code Explanation ]**

```java
public class Solution {
    public long splitArray(int[] nums) {
        long sumA = 0, sumB = 0;

        for (int i = 0; i < nums.length; i++) {
            if (isPrime(i)) {
                sumA += nums[i]; // Prime index → array A
            } else {
                sumB += nums[i]; // Non-prime index → array B
            }
        }

        return Math.abs(sumA - sumB);
    }

    private boolean isPrime(int num) {
        if (num < 2) return false;
        if (num == 2) return true;
        if (num % 2 == 0) return false;
        for (int i = 3; i * i <= num; i += 2) {
            if (num % i == 0) return false;
        }
        return true;
    }
}
```

---

#### 🧪 **\[Sample Test Cases - ]**

```
🎤 "Let’s look at a few sample test cases."

Test Case 1:
Input: [2, 3, 4]
Prime Index: 2 → A = [4], B = [2, 3] → Output: 1

Test Case 2:
Input: [-1, 5, 7, 0]
Prime Indices: 2, 3 → A = [7, 0], B = [-1, 5] → Output: 3
```

---

#### ✅ **\[Summary ]**

```
🎤 "To summarize:
- Prime index detection is key.
- Just add elements accordingly to A or B.
- Then return the absolute difference of their sums.

This solution runs in O(n√n) worst-case due to prime checks but is fast enough for contest constraints."
```

---


---

