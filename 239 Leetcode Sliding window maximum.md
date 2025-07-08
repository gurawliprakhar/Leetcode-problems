
---

# 🪟 Sliding Window Maximum

## 📝 Problem Statement

Given an array of integers `nums` and a sliding window of size `k`, move the window from the left to the right end of the array. At each step, return the **maximum** value in the current window.

### Constraints:
- `1 <= nums.length <= 10⁵`
- `-10⁴ <= nums[i] <= 10⁴`
- `1 <= k <= nums.length`

---

## 📌 Example

### Input:
```java
nums = [1,3,-1,-3,5,3,6,7], k = 3
```

### Output:
```java
[3,3,5,5,6,7]
```

### Explanation:

| Window             | Max |
|--------------------|-----|
| [1, 3, -1]          | 3   |
| [3, -1, -3]         | 3   |
| [-1, -3, 5]         | 5   |
| [-3, 5, 3]          | 5   |
| [5, 3, 6]           | 6   |
| [3, 6, 7]           | 7   |

---

## 🔍 Approach

This solution uses a **brute-force sliding window** technique:

- Slide a window of size `k` across the array.
- For each window, scan all `k` elements to find the maximum.
- Store the maximum in the result array.

This approach is simple and intuitive but not optimal for large inputs.

---

## 💻 Code

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        int[] res = new int[n - k + 1];

        for (int i = 0; i <= n - k; i++) {
            int max = nums[i];
            for (int j = 1; j < k; j++) {
                max = max(max, nums[i + j]);
            }
            res[i] = max;
        }
        return res;
    }

    private int max(int a, int b) {
        return a > b ? a : b;
    }
}
```

---

## 🧪 Dry Run

Let’s dry-run the input `nums = [1,3,-1,-3,5,3,6,7]`, `k = 3`:

- `i = 0`: window = [1, 3, -1] → max = 3
- `i = 1`: window = [3, -1, -3] → max = 3
- `i = 2`: window = [-1, -3, 5] → max = 5
- `i = 3`: window = [-3, 5, 3] → max = 5
- `i = 4`: window = [5, 3, 6] → max = 6
- `i = 5`: window = [3, 6, 7] → max = 7

Final result: `[3, 3, 5, 5, 6, 7]`

---

## ⏱️ Time & Space Complexity

| Metric        | Complexity     |
|---------------|----------------|
| Time          | O(n * k)       |
| Space         | O(n - k + 1)   |

---

## ✅ When to Use This Approach

- When `k` is small
- When simplicity is preferred over performance
- For educational purposes or initial prototyping

---

