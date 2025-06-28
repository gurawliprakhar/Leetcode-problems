

---

## 📌 Problem Summary

Given an integer array `nums` and an integer `k`, the task is to **find a subsequence of length `k` that has the largest sum**, while **preserving the original order** of elements.

---

### ✅ What is a Subsequence?

A **subsequence** keeps the **relative order of elements** but allows skipping elements.
For example:

* ✅ Valid subsequence of `[2, 1, 3, 3]`: `[2, 3]`
* ❌ Not valid: `[3, 2]` (because order changed)

---

## 🧪 Example Test Cases:

| Input                            | Output               | Explanation              |
| -------------------------------- | -------------------- | ------------------------ |
| `nums = [2, 1, 3, 3]`, `k = 2`   | `[3, 3]`             | Largest possible sum = 6 |
| `nums = [-1, -2, 3, 4]`, `k = 3` | `[-1, 3, 4]`         | Largest possible sum = 6 |
| `nums = [3, 4, 3, 3]`, `k = 2`   | `[3, 4]` or `[4, 3]` | Both sum to 7            |

---

## ✅ Java Solution

### Full Code:

```java
public class Solution {

    public int[] maxSubsequence(int[] nums, int k) {
        if (k == nums.length) return nums;

        int[] temp = nums.clone();
        bubbleSort(temp);

        int kLarg = temp[temp.length - k];
        int count = 0;
        for (int i = temp.length - k; i < temp.length; i++) {
            if (temp[i] == kLarg) count++;
        }

        int[] res = new int[k];
        int idx = 0;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > kLarg) {
                res[idx++] = nums[i];
            } else if (nums[i] == kLarg && count > 0) {
                res[idx++] = nums[i];
                count--;
            }
            if (idx == k) break;
        }
        return res;
    }

    public void bubbleSort(int[] ar) {
        for (int i = 0; i < ar.length - 1; i++) {
            for (int j = 0; j < ar.length - i - 1; j++) {
                if (ar[j] > ar[j + 1]) {
                    int temp = ar[j];
                    ar[j] = ar[j + 1];
                    ar[j + 1] = temp;
                }
            }
        }
    }
}
```

---

## ✅ Dry Run Explanation 📖

### Step 1: Handle k equals array length

```java
if (k == nums.length) return nums;
```

Shortcut for when the full array is the only possible subsequence.

---

### Step 2: Create a Copy Before Sorting

```java
int[] temp = nums.clone();
```

This preserves the original array so we don't lose element order.

---

### Step 3: Sort the Copy (Bubble Sort for educational purpose)

```java
bubbleSort(temp);
```

Bubble Sort sorts `temp` in ascending order.
(For large inputs, replace with `Arrays.sort()` for O(n log n) performance.)

---

### Step 4: Identify the K-th Largest Number (`kLarg`)

```java
int kLarg = temp[temp.length - k];
```

This helps filter elements to keep in the final result.

---

### Step 5: Count How Many Times kLarg Appears in Top-K Elements

```java
for (int i = temp.length - k; i < temp.length; i++) {
    if (temp[i] == kLarg) count++;
}
```

To avoid over-picking duplicate elements later.

---

### Step 6: Build the Result Array (Original Order Preserved)

```java
for (int i = 0; i < nums.length; i++) {
    if (nums[i] > kLarg) {
        res[idx++] = nums[i];
    } else if (nums[i] == kLarg && count > 0) {
        res[idx++] = nums[i];
        count--;
    }
    if (idx == k) break;
}
```

✅ Pick all elements **larger than `kLarg`**
✅ Pick **only limited `kLarg` copies**
✅ Stop when exactly `k` elements collected.

---

## ✅ Time Complexity

| Part                       | Complexity                                             |
| -------------------------- | ------------------------------------------------------ |
| Bubble Sort                | O(n²)                                                  |
| Counting & Building Result | O(n)                                                   |
| **Total**                  | O(n²) (can be improved to O(n log n) with faster sort) |

---

## ✅ Optimization Tip 💡

For large inputs, replace bubble sort with:

```java
Arrays.sort(temp);
```

---

## ✅ Summary

This problem combines:

* Sorting
* Frequency counting
* Careful filtering
* Order-preserving subsequence logic

Great for practicing **array manipulation** and **algorithmic thinking** in Java.

---

If this explanation helped you, feel free to ⭐ star this repository and follow for more LeetCode dry runs and Java solutions!

---

