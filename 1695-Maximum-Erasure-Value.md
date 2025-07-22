

---

## 📘 **README Content (Hinglish)**

```md
# 🔥 Leetcode 1695: Maximum Erasure Value (Hinglish Explanation)

## 📌 Problem Statement

Aapko ek array `nums` diya gaya hai jisme positive integers hain.  
Aapko ek aisa **subarray** choose karna hai jisme **koi bhi element repeat na ho**  
Aur us subarray ka **sum maximum** ho.

Subarray matlab — **contiguous** elements (ek ke baad ek).

---

## 🧪 Example

**Input:**
```

nums = \[4, 2, 4, 5, 6]

```

**Output:**
```

17

````

**Explanation:**
Best subarray hai `[2, 4, 5, 6]` jiska sum hai `17`.

---

## 💡 Approach: Sliding Window + HashSet

Yeh ek classic **Sliding Window problem** hai.

### 🔧 Steps:
- Do pointers `left` aur `right` lenge — window banane ke liye
- Ek `HashSet` lenge taaki pata chale kaunsa element window mein hai
- Agar duplicate milta hai toh `left` pointer ko aage badhaake purane elements hata denge
- Saath hi `currentSum` aur `maxSum` update karte rahenge

---

## 💻 Java Code (with Explanation)

```java
import java.util.HashSet;

public class Solution {
    public int maximumUniqueSubarray(int[] nums) {
        int left = 0, right = 0;
        int currentSum = 0, maxSum = 0;
        HashSet<Integer> seen = new HashSet<>();

        while (right < nums.length) {
            while (seen.contains(nums[right])) {
                seen.remove(nums[left]);
                currentSum -= nums[left];
                left++;
            }
            seen.add(nums[right]);
            currentSum += nums[right];
            maxSum = Math.max(maxSum, currentSum);
            right++;
        }

        return maxSum;
    }
}
````

---

## 🧠 Dry Run with `[4, 2, 4, 5, 6]`

1. 4 unique → add → sum = 4
2. 2 unique → add → sum = 6
3. 4 repeat → remove 4 from left → sum = 2 → add 4 again → sum = 6
4. 5 → add → sum = 11
5. 6 → add → sum = 17 ✅

👉 Final max sum = **17**

---

## ⏱ Time & Space Complexity

* **Time:** O(n) – har element sirf ek baar add/remove hota hai
* **Space:** O(n) – HashSet ke liye

---

## 🔗 Useful Links

* 🔗 [Leetcode Problem Link](https://leetcode.com/problems/maximum-erasure-value/)
* 📘 [Mera Discuss Solution (with Explanation)](https://leetcode.com/problems/maximum-erasure-value/solutions/6988615/1695-maximum-erasure-value-using-the-sliding-window-hashset-approach/)

---



---


