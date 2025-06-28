
---

```markdown
# 🧩 LeetCode Problem 88: Merge Sorted Array

## 📜 Problem Statement

You are given two integer arrays `nums1` and `nums2`, sorted in **non-decreasing** order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2`, respectively.

Merge `nums1` and `nums2` into a single array **sorted in non-decreasing order**.  
The final sorted array should be stored **inside** `nums1`.

👉 Note:  
- `nums1` has a length of `m + n`, where the first `m` elements denote the elements to be merged, and the last `n` elements are set to 0 and should be ignored.
- `nums2` has a length of `n`.

---

## 🧠 Approach: Two-Pointer Merge (with Extra Space)

1. Use three pointers: `i` for `nums1`, `j` for `nums2`, and `k` for the merged array `res`.
2. Compare values in both arrays from the start and insert the smaller value into `res`.
3. After the merge, copy the result back into `nums1`.

This approach is easy to implement and useful when practicing merge logic, especially when space constraints are relaxed.

---

## 🔍 Dry Run Example

**Input:**
```
nums1 = [1,2,3,0,0,0], m = 3  
nums2 = [2,5,6], n = 3
```

**Step-by-step Merge:**

| i | j | res               | Comment                              |
|---|---|-------------------|--------------------------------------|
| 0 | 0 | [1]               | 1 < 2 → take nums1[0]                |
| 1 | 0 | [1,2]             | 2 == 2 → take nums1[1]               |
| 2 | 0 | [1,2,2]           | 3 > 2 → take nums2[0]                |
| 2 | 1 | [1,2,2,3]         | 3 < 5 → take nums1[2]                |
| - | 1 | [1,2,2,3,5,6]     | nums1 exhausted, copy rest of nums2  |

Final result gets copied back into `nums1`:  
```java
nums1 = [1,2,2,3,5,6];
```

---

## ✅ Code

```java
import java.util.Arrays;

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int[] res = new int[m + n];
        int i = 0, j = 0, k = 0;

        while (i < m && j < n) {
            if (nums1[i] <= nums2[j]) {
                res[k++] = nums1[i++];
            } else {
                res[k++] = nums2[j++];
            }
        }

        while (i < m) {
            res[k++] = nums1[i++];
        }

        while (j < n) {
            res[k++] = nums2[j++];
        }

        // Copy merged result back into nums1
        for (int x = 0; x < m + n; x++) {
            nums1[x] = res[x];
        }

        // For visual confirmation during development
        System.out.println(Arrays.toString(nums1));
    }
}
```

---

## 💡 Additional Notes

- This solution uses **O(m + n)** extra space.
- If space is a concern, you can implement an **in-place reverse merge** strategy using three pointers from the end.

```

