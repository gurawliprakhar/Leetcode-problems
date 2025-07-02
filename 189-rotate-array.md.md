
---

```markdown
# 🔄 Rotate Array

## 🧩 Problem Statement

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

### Constraints:
- `1 <= nums.length <= 10⁵`
- `-2³¹ <= nums[i] <= 2³¹ - 1`
- `0 <= k <= 10⁵`

---

## 📥 Example

### Input:
```java
nums = [1, 2, 3, 4, 5, 6, 7]
k = 3
```

### Output:
```java
[5, 6, 7, 1, 2, 3, 4]
```

### Explanation:
- Rotate 1 step: [7, 1, 2, 3, 4, 5, 6]  
- Rotate 2 steps: [6, 7, 1, 2, 3, 4, 5]  
- Rotate 3 steps: [5, 6, 7, 1, 2, 3, 4]

---

## 💡 Approach: In-Place Reversal (Two Pointers)

To rotate the array in-place with **O(1)** extra space, we use the **three-step reversal** technique:

1. **Reverse the entire array**
2. **Reverse the first `k` elements**
3. **Reverse the remaining `n - k` elements**

### 🔁 Why `k %= n`?
If `k > n`, rotating `k` times is equivalent to rotating `k % n` times.  
Example: rotating an array of length 7 by 10 steps is the same as rotating it by 3 steps.

---

## 🧪 Dry Run

### Input:
```java
nums = [1, 2, 3, 4, 5, 6, 7], k = 3
```

### Step 1: Normalize `k`
```java
k = k % n = 3 % 7 = 3
```

### Step 2: Reverse Entire Array
```java
Before: [1, 2, 3, 4, 5, 6, 7]
After:  [7, 6, 5, 4, 3, 2, 1]
```

### Step 3: Reverse First `k = 3` Elements
```java
Before: [7, 6, 5, 4, 3, 2, 1]
After:  [5, 6, 7, 4, 3, 2, 1]
```

### Step 4: Reverse Remaining `n - k = 4` Elements
```java
Before: [5, 6, 7, 4, 3, 2, 1]
After:  [5, 6, 7, 1, 2, 3, 4]
```

✅ Final Output: `[5, 6, 7, 1, 2, 3, 4]`

---

## 🧠 Time & Space Complexity

| Metric            | Value     |
|-------------------|-----------|
| Time Complexity   | O(n)      |
| Space Complexity  | O(1)      |

---

## 🧾 Java Code

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k %= n;

        reverse(nums, 0, n - 1);     // Step 1
        reverse(nums, 0, k - 1);     // Step 2
        reverse(nums, k, n - 1);     // Step 3
    }

    private void reverse(int[] nums, int i, int j) {
        while (i < j) {
            int temp = nums[i];
            nums[i++] = nums[j];
            nums[j--] = temp;
        }
    }
}
```

---

## 🔗 Related Resources

- [LeetCode Problem Link](https://leetcode.com/problems/rotate-array/solutions/6910137/rotate-array-by-triprakhar-zzwb/)  
```

