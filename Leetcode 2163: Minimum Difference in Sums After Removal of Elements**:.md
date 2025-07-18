

---

### 📄 `README.md`

````markdown
# 🧮 Minimum Difference in Sums After Removal of Elements

> Leetcode 2163 | Medium  
> 🗓️ Daily Challenge: July 18, 2025  
> 💡 Tags: Greedy, Heaps, Prefix/Suffix Sums  

---

## 🧠 Problem Summary

You're given an integer array `nums` of **length `3n`**. Your task is to:

1. **Remove exactly `n` elements** from the array.
2. The remaining `2n` elements should be split into:
   - First `n` elements → `sumfirst`
   - Last `n` elements → `sumsecond`
3. Return the **minimum possible value of `sumfirst - sumsecond`** by choosing the best set of `n` elements to remove.

---

## 🔍 Example

```text
Input: nums = [7, 9, 5, 8, 1, 3]
n = 2

Try removing different combinations of 2 elements:
→ Remaining: [5, 8, 1, 3] → sumfirst = 13, sumsecond = 4 → diff = 9  
→ Remaining: [7, 5, 1, 3] → sumfirst = 12, sumsecond = 4 → diff = 8  
→ ...

Best split leads to minimum difference = ✅ **1**
````

---

## 🚀 Approach

### Step 1: Prefix Min Sum (left\[])

* Use a **max heap** to maintain the **smallest `n` values** from the **first `2n`** elements.
* Store the current sum of these `n` smallest values in `left[i]`.

### Step 2: Suffix Max Sum (right\[])

* Use a **min heap** to maintain the **largest `n` values** from the **last `2n`** elements.
* Store the current sum of these `n` largest values in `right[i]`.

### Step 3: Compare Differences

* Try all valid splits between prefix and suffix:

```java
minDiff = Math.min(minDiff, left[i] - right[i]);
```

---

## ✅ Code

```java
import java.util.Collections;
import java.util.PriorityQueue;

class Solution {
    public long minimumDifference(int[] nums) {
        int n = nums.length / 3;
        long[] left = new long[n + 1];
        long[] right = new long[n + 1];

        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        long leftSum = 0;
        for (int i = 0; i < 2 * n; i++) {
            maxHeap.add(nums[i]);
            leftSum += nums[i];
            if (maxHeap.size() > n) {
                leftSum -= maxHeap.poll();
            }
            if (i >= n - 1) {
                left[i - n + 1] = leftSum;
            }
        }

        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        long rightSum = 0;
        for (int i = 3 * n - 1; i >= n; i--) {
            minHeap.add(nums[i]);
            rightSum += nums[i];
            if (minHeap.size() > n) {
                rightSum -= minHeap.poll();
            }
            if (i <= 2 * n) {
                right[i - n] = rightSum;
            }
        }

        long minDiff = Long.MAX_VALUE;
        for (int i = 0; i <= n; i++) {
            minDiff = Math.min(minDiff, left[i] - right[i]);
        }

        return minDiff;
    }
}
```

---

## 📦 Time and Space Complexity

| Type  | Value      |
| ----- | ---------- |
| Time  | O(n log n) |
| Space | O(n)       |

---

## 📚 Learning Takeaway

This problem teaches a powerful technique:

* Smart greedy element tracking using heaps
* Prefix and suffix processing to minimize diff
* Real-world tradeoff simulation!

---

## 🔗 Related Links

* [Leetcode Problem Link](https://leetcode.com/problems/minimum-difference-in-sums-after-removal-of-elements/)


---

## 💬 Author

**Prakhar Tripathi**
📧 [gurawliprakhar@gmail.com](mailto:gurawliprakhar@gmail.com)

```
