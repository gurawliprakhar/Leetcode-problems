

---

## 🧩 Find the Maximum Length of Valid Subsequence I

> 🔗 **LeetCode:** [Find the Maximum Length of Valid Subsequence I](https://leetcode.com/problems/find-the-maximum-length-of-valid-subsequence-i/submissions/1699634026/?envType=daily-question&envId=2025-07-16)

---

### 📌 Problem Explanation (In Simple Words)

You're given an array of integers. You need to choose a **subsequence** (can skip elements, but order must stay the same) such that:

👉 **Every pair of adjacent elements in the subsequence**, when added together, always gives:

* Either all **even** sums or
* All **odd** sums

🎯 Your goal: **Return the maximum length** of such a valid subsequence.

---

### 💡 Core Idea

We only care about **odd and even (parity)**:

* Even + Even = Even
* Odd + Odd = Even
* Odd + Even = Odd
* Even + Odd = Odd

So we look for these 4 valid patterns:

1. All numbers are **even** → all sums are even ✅
2. All numbers are **odd** → all sums are even ✅
3. Alternate: **odd → even → odd → ...** → all sums are odd ✅
4. Alternate: **even → odd → even → ...** → all sums are odd ✅

We try all four and return the longest one.

---

### 🧪 Example

```java
Input:  nums = [1, 2, 3, 4]

→ Try subsequence [1, 2, 3, 4]

(1 + 2) = 3 → odd  
(2 + 3) = 5 → odd  
(3 + 4) = 7 → odd ✅

All sums are odd → Valid subsequence  
✅ Output: 4
```

---

### 💻 Java Code

```java
class Solution {
    public int maximumLength(int[] nums) {
        int allEven = getLength(nums, 0, 0);     // All evens → even sums
        int allOdd = getLength(nums, 1, 1);      // All odds → even sums
        int oddEven = getLength(nums, 1, 0);     // Alternating → odd sums
        int evenOdd = getLength(nums, 0, 1);     // Alternating → odd sums

        return Math.max(Math.max(allEven, allOdd), Math.max(oddEven, evenOdd));
    }

    private int getLength(int[] nums, int f, int s) {
        int count = 0;
        int expect = f;

        for (int num : nums) {
            int cur = num % 2;

            if (cur == expect) {
                count++;
                if (f != s) {
                    expect = (expect == f) ? s : f;
                }
            }
        }
        return count;
    }
}
```

---

### 🧵 Dry Run

Let’s dry run this input:

```java
nums = [1, 2, 3, 4]
Pattern: odd → even → odd → even
```

| Index | Num | Expecting | Num % 2 | Match? | Count | Flip Expect To |
| ----- | --- | --------- | ------- | ------ | ----- | -------------- |
| 0     | 1   | 1 (odd)   | 1       | ✅      | 1     | 0 (even)       |
| 1     | 2   | 0 (even)  | 0       | ✅      | 2     | 1 (odd)        |
| 2     | 3   | 1 (odd)   | 1       | ✅      | 3     | 0 (even)       |
| 3     | 4   | 0 (even)  | 0       | ✅      | 4     | 1 (odd)        |

✅ Final count = **4**

---

### ✅ Output

```java
Result = 4
```

---

### 🧠 Time & Space Complexity

| Metric   | Value                         |
| -------- | ----------------------------- |
| ⏱ Time   | `O(n)` — 4 linear scans       |
| 💾 Space | `O(1)` — constant extra space |

---

