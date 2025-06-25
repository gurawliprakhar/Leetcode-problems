

---

# 📈 LeetCode 2040: Kth Smallest Product of Two Sorted Arrays

[![LeetCode Problem](https://img.shields.io/badge/LeetCode-2040-orange)](https://leetcode.com/problems/kth-smallest-product-of-two-sorted-arrays/)
**Difficulty:** Hard

---

## 📌 Problem Description

Given two **sorted integer arrays** `nums1` and `nums2`, and an integer `k`, find the **k-th smallest product** formed by multiplying any element from `nums1` with any element from `nums2`.

---

### 🧑‍💻 Example:

```java
Input:
nums1 = [-4, -2, 0, 3]
nums2 = [2, 4]
k = 6

Output:
0
```

**Explanation:**
All product pairs are:

```
[-16, -8, -8, -4, 0, 0, 6, 12]
```

Sorted, the **6th smallest product** is `0`.

---

## 🚀 Algorithm Overview

Due to the large possible input size (`n`, `m` up to 50,000 elements each), **brute force is not feasible**.

### ✅ Core Idea: Binary Search on the Answer Space (Product Values)

We perform binary search over the **possible product values**, rather than array indices.

---

### ✅ Steps:

1. **Binary Search Range:**

   * Minimum possible product: `-1e10`
   * Maximum possible product: `1e10`

2. **Count Function (`countLessEqual`):**

   * For each `a` in `nums1`, binary search `nums2` to count how many `b` satisfy:

   ```
   a * b ≤ mid
   ```

   * Handle **positive**, **negative**, and **zero** cases carefully to manage inequality direction.

3. **Binary Search Process:**

   * Adjust search range based on the number of valid products ≤ `mid` until the k-th smallest product is found.

---

## ✅ Full Java Solution:

```java
public class KthSmallestProduct {
    public long kthSmallestProduct(int[] nums1, int[] nums2, long k) {
        long low = -1_000_000_000_0L;
        long high = 1_000_000_000_0L;

        while (low < high) {
            long mid = low + (high - low) / 2;
            long count = countLessEqual(nums1, nums2, mid);
            if (count >= k) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        return low;
    }

    private long countLessEqual(int[] nums1, int[] nums2, long mid) {
        long count = 0;
        for (int a : nums1) {
            if (a > 0) {
                int l = 0, r = nums2.length;
                while (l < r) {
                    int m = l + (r - l) / 2;
                    if ((long) a * nums2[m] <= mid) {
                        l = m + 1;
                    } else {
                        r = m;
                    }
                }
                count += l;
            } else if (a < 0) {
                int l = 0, r = nums2.length;
                while (l < r) {
                    int m = l + (r - l) / 2;
                    if ((long) a * nums2[m] <= mid) {
                        r = m;
                    } else {
                        l = m + 1;
                    }
                }
                count += nums2.length - l;
            } else {  // a == 0
                if (mid >= 0) count += nums2.length;
            }
        }
        return count;
    }
}
```

---

## ⏱️ Time Complexity:

| Part                        | Complexity              |
| --------------------------- | ----------------------- |
| Binary Search (Value Space) | `O(log(range)) ≈ O(60)` |
| For each element in nums1   | `O(n)`                  |
| Binary Search on nums2      | `O(log m)`              |

### ✅ Total Complexity:

```
O(n * log m * log range)
```

Where:

* `n = nums1.length`
* `m = nums2.length`
* `range ≈ 2e10`

---

## ✅ Key Learnings:

* Binary search **can be used on value space**, not just indices.
* Careful sign handling is critical when working with inequalities on products.
* Think in terms of **"decision problem" inside binary search"**:
  For each guess `mid`, "Are there at least `k` products ≤ `mid`?"

---

## ✅ Related Problems:

* [LeetCode 373: Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/)
* [LeetCode 378: Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)

---

## 📚 References:

* [Official LeetCode Problem Link](https://leetcode.com/problems/kth-smallest-product-of-two-sorted-arrays/)

---

## ✅ Author:

**Prakhar Tripathi**

---

If you found this helpful, don’t forget to ⭐ star the repo and follow for more LeetCode solutions with full explanations!

---
