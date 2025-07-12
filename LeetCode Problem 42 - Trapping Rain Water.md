
---

## 🌧️ LeetCode Problem #42: Trapping Rain Water

### 📖 Problem Statement

> Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

---

### 🧙‍♂️ Problem Story – *The Rain Wizard's Challenge*

Imagine a wizard visiting your town, conjuring rainstorms to test your ingenuity. Each house on the street has a different height, forming a skyline. After the rains, puddles form between taller buildings, and your task is to tell the wizard **exactly how much water is trapped**.

This isn't just magic—it's logic.

---

### 🌟 Example

**Input**:  
`height = [0,1,0,2,1,0,1,3,2,1,2,1]`

**Visualization**:  
```
        █
    █   █
█   █ █ █   █
█ █ █ █ █ █ █
──────────────
```

**Output**: `6` units of trapped water

---

### 🔍 Approach: Two-Pointer Technique

We use two pointers (`i` and `j`) from both ends of the array. By tracking the highest bars (`lmax` and `rmax`) from either side, we can decide how much water can be stored above each bar at position `i` or `j`.

---

### 🧑‍💻 Java Code

```java
class Solution {
    public int trap(int[] height) {
        int i = 0, j = height.length - 1;
        int lmax = 0, rmax = 0;
        int total = 0;

        while (i < j) {
            if (height[i] < height[j]) {
                if (height[i] >= lmax) {
                    lmax = height[i];
                } else {
                    total += lmax - height[i];
                }
                i++;
            } else {
                if(height[j] >= rmax) {
                    rmax = height[j];
                } else {
                    total += rmax - height[j];
                }
                j--;
            }
        }
        return total;
    } 
}
```

---

### 🧵 Detailed Dry Run

Let’s trace what happens with the input `[0,1,0,2,1,0,1,3,2,1,2,1]`:

| Step | i | j | height[i] | height[j] | lmax | rmax | Action                             | total |
|------|---|---|-----------|-----------|------|------|------------------------------------|--------|
| 1    | 0 |11 | 0         | 1         | 0    | 0    | height[i] < height[j], lmax=0      | 0      |
| 2    | 1 |11 | 1         | 1         | 1    | 0    | height[i] ≥ lmax → update lmax     | 0      |
| 3    | 2 |11 | 0         | 1         | 1    | 0    | total += 1 - 0 → 1                 | 1      |
| 4    | 3 |11 | 2         | 1         | 2    | 0    | height[i] ≥ lmax → update lmax     | 1      |
| 5    | 4 |11 | 1         | 1         | 2    | 0    | total += 2 - 1 → 1                 | 2      |
| 6    | 5 |11 | 0         | 1         | 2    | 0    | total += 2 - 0 → 2                 | 4      |
| 7    | 6 |11 | 1         | 1         | 2    | 0    | total += 2 - 1 → 1                 | 5      |
| 8    | 7 |11 | 3         | 1         | 3    | 0    | height[i] ≥ lmax → update lmax     | 5      |
| 9    | 8 |11 | 2         | 1         | 3    | 0    | total += 3 - 2 → 1                 | 6      |

Loop ends when `i ≥ j`. Final answer: **6 units**

---

### 💬 Final Thoughts

This two-pointer solution runs in **O(n)** time and **O(1)** space, making it a great blend of logic and efficiency. 🧠

---

