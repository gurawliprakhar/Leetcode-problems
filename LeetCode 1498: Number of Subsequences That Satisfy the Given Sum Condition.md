
---

# 🚀 LeetCode 1498: Number of Subsequences That Satisfy the Given Sum Condition

Welcome! This repository contains my Java solution for **LeetCode 1498 - Number of Subsequences That Satisfy the Given Sum Condition**, along with a detailed explanation, approach breakdown, example walkthroughs, and a dry run.

---

## 📚 Problem Explanation

### Problem Statement:

Given:

* An array of integers `nums`
* An integer `target`

You need to **count the number of non-empty subsequences** such that:

```
(minimum element in subsequence) + (maximum element in subsequence) ≤ target
```

---

### ⚡ Definitions:

* **Subsequence**: A sequence that can be derived by deleting some (or no) elements from the array without changing the relative order of the remaining elements.
* **Non-empty**: The subsequence must contain at least one element.
* **Minimum & Maximum in Subsequence**: Pick any subset, get its smallest and largest elements.

---

### ❗ Constraints:

* `1 ≤ nums.length ≤ 10^5`
* `1 ≤ nums[i] ≤ 10^6`
* `1 ≤ target ≤ 10^6`

Since the output can be large, **return the result modulo** $10^9 + 7$.

---

## 💡 Approach: Two-Pointer + Precomputing Powers of 2

### Key Idea:

After sorting the array:

For every valid window `[l, r]` (where `l <= r` and `nums[l] + nums[r] ≤ target`):

* Number of possible subsequences between index `l` and `r` = $2^{(r - l)}$

**Why?**

Because every element between `l` and `r` has two choices:
**Include** or **Don't include**
(except that `nums[l]` and `nums[r]` must exist as bounds for min and max)

---

### ✅ Algorithm Steps:

1. **Sort the Array**
   So we can easily track min and max using two pointers.

2. **Precompute Powers of 2 up to `n`**
   To quickly calculate how many subsequences exist between two indices.

3. **Two-Pointer Traversal:**
   Start `l = 0`, `r = n - 1` and move pointers inward:

* If `nums[l] + nums[r] ≤ target`:
  Count all subsequences between `l` and `r`, move `l++`

* Else:
  Move `r--`

4. **Take Modulo $10^9 + 7$** at every step to avoid overflow.

---

## 🧪 Example Walkthrough:

### Input:

```text
nums = [3, 5, 6, 7]
target = 9
```

### Step 1: Sort the Array:

```text
[3, 5, 6, 7]
```

### Step 2: Precompute Powers of 2:

We need powers of 2 up to `n = 4`:

| i | pow2\[i] = 2^i % mod |
| - | -------------------- |
| 0 | 1                    |
| 1 | 2                    |
| 2 | 4                    |
| 3 | 8                    |

So:
`pow2 = [1, 2, 4, 8]`

---

### Step 3: Two Pointer Traversal:

| l | r | nums\[l] + nums\[r] | Action                      | res |
| - | - | ------------------- | --------------------------- | --- |
| 0 | 3 | 3+7=10 > 9          | r-- → r=2                   | 0   |
| 0 | 2 | 3+6=9 ≤ 9           | res += pow2\[2-0]=4 → res=4 | 4   |
| 1 | 2 | 5+6=11 > 9          | r-- → r=1                   | 4   |
| 1 | 1 | 5+5=10 > 9          | r-- → r=0                   | 4   |

Final Result: `4`

---

### ✅ Explanation of Result:

Valid subsequences where (min + max ≤ target):

* \[3]
* \[3,5]
* \[3,6]
* \[3,5,6]

✔️ Output matches expected.

---

## 🖥️ Java Code Implementation:

```java
import java.util.Arrays;

class Solution {
    public int numSubseq(int[] nums, int target) {
        int mod = 1_000_000_007;
        Arrays.sort(nums);
        int n = nums.length;

        // Precompute powers of 2
        int[] pow2 = new int[n];
        pow2[0] = 1;
        for (int i = 1; i < n; i++) {
            pow2[i] = (pow2[i - 1] * 2) % mod;
        }

        int res = 0;
        int l = 0, r = n - 1;

        while (l <= r) {
            if (nums[l] + nums[r] <= target) {
                res = (res + pow2[r - l]) % mod;
                l++;
            } else {
                r--;
            }
        }

        return res;
    }
}
```

---

## 🕒 Time Complexity:

| Step                  | Complexity    |
| --------------------- | ------------- |
| Sorting               | $O(n \log n)$ |
| Two-pointer traversal | $O(n)$        |
| Precomputing powers   | $O(n)$        |

**Overall:**

$$
O(n \log n)
$$

---

## ✅ Space Complexity:

$$
O(n)
$$

(For the power array)

---

## 🧠 Key Takeaways:

* **Two-pointer + Sorting** works well for range-based problems with sorted conditions.
* **Precomputing powers of 2** avoids recomputation and saves time on large inputs.
* **Modulo math** is essential when working with huge result sizes in coding interviews.

---

## ✅ Tags:

`#LeetCode` `#TwoPointers` `#Java` `#Combinatorics` `#Arrays` `#Sorting` `#BinaryExponentiation`

---

## ✅ More Solutions Coming Soon!

If you liked this, ⭐️ star this repo!
I’ll keep adding more **Java LeetCode solutions with detailed dry runs and explanations**.

---


