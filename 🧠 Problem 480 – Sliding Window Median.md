# 🧠 Problem 480 – Sliding Window Median

## 📌 Problem Statement
Given an array of integers `nums` and an integer `k`, there is a sliding window of size `k` moving from the left to the right end of the array. Each time the window moves one position, compute the **median** of the numbers within the window.

The median:
- If window size `k` is odd → middle element
- If `k` is even → average of the two middle elements

Return an array of medians, one for each window movement.

### ✅ Constraints
- `1 <= k <= nums.length <= 10^5`
- `-2^31 <= nums[i] <= 2^31 - 1`

---

## 🧪 Dry Run – Example

```text
nums = [1, 3, -1, -3, 5, 3, 6, 7], k = 3

Window         → Sorted         → Median
[1,3,-1]       → [-1,1,3]       → 1.0
[3,-1,-3]      → [-3,-1,3]      → -1.0
[-1,-3,5]      → [-3,-1,5]      → -1.0
[-3,5,3]       → [-3,3,5]       → 3.0
[5,3,6]        → [3,5,6]        → 5.0
[3,6,7]        → [3,6,7]        → 6.0

🔚 Output: [1.0, -1.0, -1.0, 3.0, 5.0, 6.0]
```markdown
## 👨‍💻 Code – P

```java
class Solution {
    public double[] medianSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        double[] ans = new double[n - k + 1];
        List<Integer> window = new ArrayList<>();

        for (int i = 0; i < k; i++) {
            window.add(nums[i]);
        }
        Collections.sort(window);
        ans[0] = getMedian(window, k);

        for (int i = k; i < n; i++) {
            int out = nums[i - k];
            int idx = binarySearch(window, out);
            window.remove(idx);

            int in = nums[i];
            int insertIdx = binarySearch(window, in);
            if (insertIdx < 0) insertIdx = -insertIdx - 1;
            window.add(insertIdx, in);

            ans[i - k + 1] = getMedian(window, k);
        }
        return ans;  
    }

    private double getMedian(List<Integer> window, int k) {
        if (k % 2 == 1) {
            return window.get(k / 2);
        } else {
            return ((double) window.get(k / 2 - 1) + window.get(k / 2)) / 2.0;
        }
    }

    private int binarySearch(List<Integer> list, int target) {
        int l = 0, r = list.size() - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            int midVal = list.get(mid);
            if (midVal == target) {
                return mid;
            } else if (midVal < target) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return -l - 1;
    }
}
```
```
```markdown
## 🧪 Full Dry Run – Problem 480: Sliding Window Median

### 📥 Input
```text
nums = [1, 3, -1, -3, 5, 3, 6, 7]
k = 3
```

### 🔍 Sliding Window Process


| Step | Window (unsorted) | Sorted Window     | Removed | Inserted | Median |
|------|--------------------|-------------------|---------|----------|--------|
| 0    | [1, 3, -1]         | [-1, 1, 3]        | -       | -        | 1.0    |
| 1    | [3, -1, -3]        | [-3, -1, 3]       | 1       | -3       | -1.0   |
| 2    | [-1, -3, 5]        | [-3, -1, 5]       | 3       | 5        | -1.0   |
| 3    | [-3, 5, 3]         | [-3, 3, 5]        | -1      | 3        | 3.0    |
| 4    | [5, 3, 6]          | [3, 5, 6]         | -3      | 6        | 5.0    |
| 5    | [3, 6, 7]          | [3, 6, 7]         | 5       | 7        | 6.0    |

### ✅ Final Output
```text
[1.0, -1.0, -1.0, 3.0, 5.0, 6.0]
```


```

