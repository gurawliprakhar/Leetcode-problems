

---

```markdown
# 🧮 LeetCode Problem 169: Majority Element

## 📘 Problem Statement

Given an array `nums` of size `n`, return the **majority element**.

- The majority element is the element that appears **more than ⌊n / 2⌋ times**.
- You may assume that the majority element **always exists** in the array.

🔗 [View on LeetCode](https://leetcode.com/problems/majority-element)

---

## 🧠 Approach: Brute Force

### 🔍 Intuition
We check each element in the array and count how many times it appears. If its count exceeds `n / 2`, we return it.

### 🛠️ Algorithm Steps
1. Loop through each element `nums[i]`.
2. For each `nums[i]`, loop again through the array to count its frequency.
3. If the count exceeds `n / 2`, return `nums[i]`.

---

## 💻 Code (Java)

```java
class Solution {
    public int majorityElement(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            int count = 0;

            for (int j = 0; j < nums.length; j++) {
                if (nums[j] == nums[i]) {
                    count++;
                }
            }

            if (count > nums.length / 2) {
                return nums[i];
            }
        }

        return -1; // This line won't be reached due to problem guarantee
    }
}
```

---

## 🧪 Dry Run Example

### Input:
```java
nums = [2, 2, 1, 1, 1, 2, 2]
```

### Execution:
- i = 0 → nums[i] = 2  
  → count = 4 (2 appears 4 times)  
  → 4 > 7/2 = 3.5 → ✅ return 2

---

## 📊 Complexity Analysis

| Metric            | Value     |
|-------------------|-----------|
| Time Complexity   | O(n²)     |
| Space Complexity  | O(1)      |

---

## ✅ Sample Test Cases

| Input               | Output |
|---------------------|--------|
| [3, 2, 3]           | 3      |
| [2, 2, 1, 1, 1, 2, 2] | 2    |

---

## 📌 Notes
- This is a brute force solution. For large inputs, consider optimizing using a HashMap or the Boyer-Moore Voting Algorithm.
```

---

