
---

### 🏃‍♂️ Jump Game — Problem Explanation

You're given an array of non-negative integers called `nums`. Each element in the array represents the **maximum number of steps** you can jump forward from that position.

- You start at the **first index** (index `0`).
- Your goal is to determine whether you can **reach the last index** of the array.

---

### 📦 Example

#### Input:
```java
nums = [2, 3, 1, 1, 4]
```

#### Explanation:
- Start at index 0. You can jump up to 2 steps → try index 1 or 2.
- From index 1, you can jump 3 steps → reach index 4.
- Index 4 is the last index → ✅ You can reach the end.

#### Output:
```java
true
```

---

### ❌ Counter Example

#### Input:
```java
nums = [3, 2, 1, 0, 4]
```

#### Explanation:
- Start at index 0 → max reach is index 3.
- But index 3 has value 0 → you’re stuck.
- You can’t reach index 4 → ❌ return `false`.

---

### 🧠 Key Insight
The problem is about **reachability**. At each step, you want to track how far you can go and make sure you never get stuck before reaching the end.

 **example walkthrough** of your solution using the input:

---

### 🔢 Input: `nums = [2, 3, 1, 1, 4]`

This means:
- At index 0, you can jump up to 2 steps.
- At index 1, you can jump up to 3 steps.
- At index 2, you can jump up to 1 step.
- At index 3, you can jump up to 1 step.
- At index 4, you can jump up to 4 steps (but it's the last index).

---

### 🧭 Step-by-Step Execution

| Index `i` | `nums[i]` | `i + nums[i]` | `far` before | `far` after update | Can proceed? |
|-----------|-----------|---------------|---------------|---------------------|----------------|
| 0         | 2         | 0 + 2 = 2     | 0             | max(0, 2) = 2       | ✅ Yes         |
| 1         | 3         | 1 + 3 = 4     | 2             | max(2, 4) = 4       | ✅ Yes         |
| 2         | 1         | 2 + 1 = 3     | 4             | max(4, 3) = 4       | ✅ Yes         |
| 3         | 1         | 3 + 1 = 4     | 4             | max(4, 4) = 4       | ✅ Yes         |
| 4         | 4         | 4 + 4 = 8     | 4             | max(4, 8) = 8       | ✅ Yes         |

- At every step, `i <= far`, so we never get stuck.
- We reach the last index (and even beyond it in theory).

---

### ✅ Final Output: `true`

You can reach the last index!
 your code step-by-step using the input:

---

### 🔢 Input: `nums = [3, 2, 1, 0, 4]`

This means:
- At index 0, you can jump up to 3 steps.
- At index 1, you can jump up to 2 steps.
- At index 2, you can jump up to 1 step.
- At index 3, you can jump 0 steps.
- At index 4, you can jump 4 steps (but you may never reach it).

---

### 🧭 Step-by-Step Execution

| Index `i` | `nums[i]` | `i + nums[i]` | `far` before | `far` after update | Can proceed? |
|-----------|-----------|---------------|---------------|---------------------|----------------|
| 0         | 3         | 0 + 3 = 3     | 0             | max(0, 3) = 3       | ✅ Yes         |
| 1         | 2         | 1 + 2 = 3     | 3             | max(3, 3) = 3       | ✅ Yes         |
| 2         | 1         | 2 + 1 = 3     | 3             | max(3, 3) = 3       | ✅ Yes         |
| 3         | 0         | 3 + 0 = 3     | 3             | max(3, 3) = 3       | ✅ Yes         |
| 4         | 4         | 4 + 4 = 8     | 3             | —                   | ❌ No → return `false` |

---

### ❌ Final Output: `false`

You get stuck at index 3 because `nums[3] = 0`, and `far = 3`, so you **can’t reach index 4**.

---

# Code
```java []
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        int far = 0;

        for (int i = 0; i < n; i++) {
            if (i > far) {
                return false;
            }

            far = max(far, i + nums[i]);
        }
        return true;
    }

    public int max(int a, int b) {
        if (a > b) {
            return a;
        } else {
            return b;
        }
    }
}
```
