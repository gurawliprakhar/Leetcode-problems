### 📘 Problem Statement: Jump Game II

You are given a **0-indexed array** of integers `nums` of length `n`. Each element `nums[i]` represents the **maximum number of steps** you can jump forward from that index.

Your goal is to determine the **minimum number of jumps** required to reach the **last index** of the array, starting from the first index (`nums[0]`).

---

### 🧩 Rules

- From index `i`, you can jump to any index in the range `[i + 1, i + nums[i]]`.
- You are guaranteed that it is always possible to reach the last index.

---

### 🧪 Examples

#### Example 1:
```plaintext
Input: nums = [2, 3, 1, 1, 4]
Output: 2
Explanation:
- Jump from index 0 to index 1 (nums[0] = 2 allows jump to 1 or 2)
- Then jump from index 1 to index 4 (nums[1] = 3 allows jump to 2, 3, or 4)
```

#### Example 2:
```plaintext
Input: nums = [2, 3, 0, 1, 4]
Output: 2
Explanation:
- Jump from index 0 to index 1
- Then jump from index 1 to index 4
```

---

### ✅ Constraints

- `1 <= nums.length <= 10⁴`
- `0 <= nums[i] <= 1000`
- It is guaranteed that you can reach the last index.

---


# Intuition
### 💡 Intuition

When you first look at the problem, it seems like a dynamic programming challenge—trying to find the minimum number of steps to reach the end. But because you're allowed to jump up to `nums[i]` steps from each index, you can think of it as exploring a **range of reachable indices** at each step.

The key realization is:  
> Instead of trying all paths, we can **greedily** jump to the farthest index reachable within the current jump range.

This transforms the problem from exponential (brute force) to linear time.


# Approach
### 🛠️ Approach

We use a **greedy strategy** to minimize the number of jumps:

1. **Track the farthest index** we can reach while iterating through the array.
2. Maintain a `currentEnd` which marks the end of the range for the current jump.
3. When we reach `currentEnd`, it means we must make a jump, so we:
   - Increment the jump counter.
   - Update `currentEnd` to the farthest index we can reach so far.
4. We stop iterating at `nums.length - 2` because we don’t need to jump from the last index.

This approach ensures that at each step, we make the **locally optimal choice** (jumping to the farthest reachable index), which leads to a **globally optimal solution**.

---

# Complexity
### 📊 Complexity

- **Time complexity:** $$O(n)$$  
  We iterate through the array exactly once, updating the farthest reachable index and jump count as needed.

- **Space complexity:** $$O(1)$$  
  We use only a few integer variables (`jump`, `curEnd`, `far`) regardless of the input size, so the space usage is constant.



# Code
```java []
class Solution {
    public int jump(int[] nums) {
        int jump = 0;
        int curEnd = 0;
        int far = 0;

        for (int i = 0; i < nums.length - 1; i++) {
            far = max(far, i + nums[i]);

            if (i == curEnd) {
                jump++;
                curEnd = far;
            }
        }
        return jump;
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

Let's dry run just this line inside the loop:

```java
far = max(far, i + nums[i]);
```

This line updates the **farthest index** we can reach from the current index `i`. Here's how it behaves step-by-step for the input:

### Input: `nums = [2, 3, 1, 1, 4]`

We’ll track the values of `i`, `nums[i]`, `i + nums[i]`, and `far`:

| i | nums[i] | i + nums[i] | far before | far after (max) |
|---|---------|-------------|------------|-----------------|
| 0 | 2       | 0 + 2 = 2   | 0          | max(0, 2) = 2   |
| 1 | 3       | 1 + 3 = 4   | 2          | max(2, 4) = 4   |
| 2 | 1       | 2 + 1 = 3   | 4          | max(4, 3) = 4   |
| 3 | 1       | 3 + 1 = 4   | 4          | max(4, 4) = 4   |

### 🔍 What This Line Does

- It ensures that at every step, we know the **farthest index** we can possibly reach from any of the indices we've visited so far.
- This is crucial for deciding **when to jump**, which is handled in the next part of the loop (`if (i == curEnd)`).

Let's dry run this part of the loop:

```java
if (i == curEnd) {
    jump++;
    curEnd = far;
}
```

This condition checks whether we've reached the **end of the current jump range**. If so, we must:

1. **Increment the jump count** – because we need to make a new jump.
2. **Update `curEnd`** – to the farthest index we can reach from any index in the current range.

---

### 🔍 Dry Run with `nums = [2, 3, 1, 1, 4]`

| i | curEnd | far | i == curEnd? | Action |
|---|--------|-----|--------------|--------|
| 0 | 0      | 2   | ✅ Yes        | jump = 1, curEnd = 2 |
| 1 | 2      | 4   | ❌ No         | — |
| 2 | 2      | 4   | ✅ Yes        | jump = 2, curEnd = 4 |
| 3 | 4      | 4   | ❌ No         | — |

---

### 🧠 Why This Works

- `curEnd` marks the **limit of the current jump**.
- When `i` reaches `curEnd`, we’ve explored all options within the current jump.
- So we **must jump again**, and we extend our reach to `far`.



