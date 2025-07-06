

---

### 🧩 Problem in Simple Words

You're given:
- An array of integers called `nums`
- A number `k`

Your task is to check:
> **Are there any two same numbers in the array that are at most `k` positions apart?**

If yes, return `true`.  
If not, return `false`.

---

### 🔍 Example Breakdown

#### Example 1:
```text
nums = [1, 2, 3, 1], k = 3
```
- The number `1` appears twice.
- The two `1`s are 3 positions apart (index 0 and 3).
✅ So, return `true`.

#### Example 2:
```text
nums = [1, 0, 1, 1], k = 1
```
- The number `1` appears at index 2 and 3.
- They are just 1 position apart.
✅ So, return `true`.

#### Example 3:
```text
nums = [1, 2, 3, 1, 2, 3], k = 2
```
- All duplicates are more than 2 positions apart.
❌ So, return `false`.

---


# Intuition

Here’s a clear and concise **Intuition** section you can use for your LeetCode post:

---

### 💡 Intuition

My first thought was:  
> “We need to check if the same number appears again within the last `k` elements.”

This naturally led me to think about a **sliding window** of size `k`. As we move through the array, we can keep track of the last `k` elements we've seen using a **HashSet**. If we ever see a number that’s already in the set, it means we’ve found a duplicate within the allowed distance — so we return `true`.

This approach avoids checking every pair (which would be too slow) and gives us an efficient way to solve the problem in linear time.

---


# Approach

Here’s a clear and structured **Approach** section you can use:

---

### 🛠️ Approach

We use a **sliding window** of size `k` and a **HashSet** to track the elements in the current window.

1. **Initialize** an empty `HashSet` called `window`.
2. **Iterate** through the array using index `i`:
   - If `i > k`, remove the element at index `i - k - 1` from the set. This keeps the window size at most `k`.
   - Try to add `nums[i]` to the set:
     - If it’s already in the set, we found a duplicate within distance `k` → return `true`.
     - Otherwise, add it to the set and continue.
3. If we finish the loop without finding any duplicates, return `false`.

This approach ensures we only compare elements that are at most `k` indices apart, and the `HashSet` gives us constant-time operations for add, remove, and lookup.

---


# Complexity
Here’s how you can complete the **Complexity** section:

---

### ⏱️ Complexity

- **Time complexity:** $$O(n)$$  
  We iterate through the array once, and each operation on the `HashSet` (add, remove, contains) takes constant time on average.

- **Space complexity:** $$O(\min(n, k))$$  
  In the worst case, the `HashSet` stores up to `k` elements — the size of the sliding window.

---




# Code
```java []
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Set<Integer> window = new HashSet<>();

        for (int i = 0; i < nums.length; i++) {
            if (i > k) {
                window.remove(nums[i - k - 1]);
            }
            if (!window.add(nums[i])) {
                return true;
            }
        }
        return false;
    }
}
```
Let's do a **dry run** of this loop:

```java
for (int i = 0; i < nums.length; i++) {
    if (i > k) {
        window.remove(nums[i - k - 1]);
    }
    if (!window.add(nums[i])) {
        return true;
    }
}
```

We'll use this input for the dry run:

```java
nums = [1, 2, 3, 1], k = 3
```

---

### 🧪 Dry Run

| i | nums[i] | i > k? | Removed Element | Set Before Add | Duplicate? | Set After Add |
|---|---------|--------|------------------|----------------|------------|----------------|
| 0 | 1       | ❌ No   | —                | {}             | ❌ No       | {1}            |
| 1 | 2       | ❌ No   | —                | {1}            | ❌ No       | {1, 2}         |
| 2 | 3       | ❌ No   | —                | {1, 2}         | ❌ No       | {1, 2, 3}      |
| 3 | 1       | ❌ No   | —                | {1, 2, 3}      | ✅ Yes      | — (return true) |

---

### 🔍 Key Insight

- The condition `i > k` ensures we only start removing elements **after** the window exceeds size `k`.
- In this case, since `k = 3`, we never remove anything because `i` never becomes greater than `3`.
- At `i = 3`, we try to add `1` again, which is already in the set → **duplicate found within distance ≤ k** → return `true`.

Let’s dry run the code on this input:

```java
nums = [1, 2, 3, 1, 2, 3], k = 2
```

---

### 🧪 Dry Run Table

| i | nums[i] | i > k? | Removed Element     | Set Before Add | Duplicate? | Set After Add |
|---|---------|--------|----------------------|----------------|------------|----------------|
| 0 | 1       | ❌ No   | —                    | {}             | ❌ No       | {1}            |
| 1 | 2       | ❌ No   | —                    | {1}            | ❌ No       | {1, 2}         |
| 2 | 3       | ❌ No   | —                    | {1, 2}         | ❌ No       | {1, 2, 3}      |
| 3 | 1       | ✅ Yes  | Remove nums[0] = 1   | {2, 3}         | ❌ No       | {2, 3, 1}      |
| 4 | 2       | ✅ Yes  | Remove nums[1] = 2   | {3, 1}         | ❌ No       | {3, 1, 2}      |
| 5 | 3       | ✅ Yes  | Remove nums[2] = 3   | {1, 2}         | ❌ No       | {1, 2, 3}      |

---

### 🔍 Final Result

- We never encounter a duplicate **within the sliding window of size `k = 2`**.
- So, the function returns `false`.
