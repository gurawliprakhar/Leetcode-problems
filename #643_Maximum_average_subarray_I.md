

---

## 📄 `maximum_average_subarray_I.md`

```markdown
# Maximum Average Subarray I

## 🧩 Problem Statement

You are given:
- An integer array `nums` of length `n`.
- An integer `k` such that `1 ≤ k ≤ n`.

**Goal:**  
Find the contiguous subarray of **exactly length `k`** that has the highest average value, and return that average as a `double`.  
Your answer should be accurate within a margin of `10⁻⁵`.

---

## 🔍 Example

### Example 1
**Input:** `nums = [1, 12, -5, -6, 50, 3]`, `k = 4`  
**Subarrays of size 4:**
- `[1, 12, -5, -6]` → Average = `0.5`
- `[12, -5, -6, 50]` → Average = `12.75` ✅
- `[-5, -6, 50, 3]` → Average = `10.5`

**Output:** `12.75`

### Example 2
**Input:** `nums = [5]`, `k = 1`  
**Output:** `5.0`

---

## 💡 Approach: Sliding Window

Instead of recalculating the sum of every new subarray:
- Compute the sum of the first `k` elements.
- Slide the window:
  - Remove the element exiting.
  - Add the element entering.

This keeps your sum update time at `O(1)` and the overall time at `O(n)`.

---

## 🚀 Java Implementation

```java
public class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int curSum = 0;
        for (int i = 0; i < k; i++) {
            curSum += nums[i];
        }

        double maxAvg = (double) curSum / k;

        for (int i = k; i < nums.length; i++) {
            int incoming = nums[i];
            int outgoing = nums[i - k];
            curSum += incoming - outgoing;

            double avg = (double) curSum / k;
            maxAvg = Math.max(maxAvg, avg);
        }

        return maxAvg;
    }
}
```

---

## 🧪 Dry Run (Detailed)

### Input: `nums = [1, 12, -5, -6, 50, 3]`, `k = 4`

| Step | Window                     | Incoming | Outgoing | Sum  | Average | Max So Far |
|------|----------------------------|----------|----------|------|---------|------------|
| Init | `[1, 12, -5, -6]`          | –        | –        | `2`  | `0.5`   | `0.5`      |
| 1    | `[12, -5, -6, 50]`         | `50`     | `1`      | `51` | `12.75` | `12.75` ✅ |
| 2    | `[-5, -6, 50, 3]`          | `3`      | `12`     | `42` | `10.5`  | `12.75` ❌ |

---

## 📊 Complexity

| Metric         | Value     |
|----------------|-----------|
| Time Complexity| `O(n)`    |
| Space Complexity| `O(1)`   |

---

## 🧠 Edge Cases
- `k = 1`: Just find the max element.
- All elements negative: Still return the highest average (least negative).
- Array length equals `k`: Return average of entire array.

---

