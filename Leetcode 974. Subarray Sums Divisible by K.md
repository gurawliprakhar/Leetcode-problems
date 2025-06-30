---

# 📊 Subarray Sums Divisible by K

## 🧩 Problem Statement

Given an integer array `nums` and an integer `k`, return the number of **non-empty subarrays** whose **sum is divisible by `k`**.

A **subarray** is a contiguous part of an array.

---

## 📌 Example

### Input:
```text
nums = [4, 5, 0, -2, -3, 1]
k = 5
```

### Output:
```text
7
```

### Explanation:
The 7 subarrays with sums divisible by 5 are:
- `[5]`
- `[5, 0]`
- `[5, 0, -2, -3]`
- `[0]`
- `[0, -2, -3]`
- `[-2, -3]`
- `[4, 5, 0, -2, -3, 1]`

---

## 🧠 Approach 1: Prefix Sum + HashMap (Optimal)

We use **prefix sums** and **modulo arithmetic** to track how many times a particular modulo value has occurred. If two prefix sums have the same modulo `k`, the subarray between them is divisible by `k`.

### Key Idea:
If `prefixSum[j] % k == prefixSum[i] % k`, then the subarray `nums[i+1..j]` is divisible by `k`.

### ✅ Java Code

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        Map<Integer, Integer> modCount = new HashMap<>();
        modCount.put(0, 1); // base case for prefix sum divisible by k
        int sum = 0, count = 0;

        for (int num : nums) {
            sum += num;
            int mod = ((sum % k) + k) % k; // normalize negative mods
            count += modCount.getOrDefault(mod, 0);
            modCount.put(mod, modCount.getOrDefault(mod, 0) + 1);
        }

        return count;
    }
}
```

### ⏱️ Complexity

| Metric         | Value     |
|----------------|-----------|
| Time Complexity| O(n)      |
| Space Complexity| O(k)     |

---

## 🧠 Approach 2: Brute-force Two-Pointer (Inefficient)

This approach uses two nested loops to check every possible subarray and count those whose sum is divisible by `k`.

### ❌ Java Code

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        int count = 0;
        for (int start = 0; start < nums.length; start++) {
            int sum = 0;
            for (int end = start; end < nums.length; end++) {
                sum += nums[end];
                if (sum % k == 0) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

### ⏱️ Complexity

| Metric         | Value     |
|----------------|-----------|
| Time Complexity| O(n²)     |
| Space Complexity| O(1)     |

---

## 🧪 Dry Run (Prefix Sum Approach)

For `nums = [4, 5, 0, -2, -3, 1]`, `k = 5`:

| Index | Num | Prefix Sum | Modulo | Count of Modulo | Total Count |
|-------|-----|-------------|--------|------------------|--------------|
| -     | -   | 0           | 0      | {0: 1}           | 0            |
| 0     | 4   | 4           | 4      | {0:1, 4:1}       | 0            |
| 1     | 5   | 9           | 4      | {0:1, 4:2}       | 1            |
| 2     | 0   | 9           | 4      | {0:1, 4:3}       | 3            |
| 3     | -2  | 7           | 2      | {0:1, 4:3, 2:1}  | 3            |
| 4     | -3  | 4           | 4      | {0:1, 4:4, 2:1}  | 6            |
| 5     | 1   | 5           | 0      | {0:2, 4:4, 2:1}  | 7            |

---

## 🧮 Constraints

- `1 <= nums.length <= 3 * 10⁴`
- `-10⁴ <= nums[i] <= 10⁴`
- `2 <= k <= 10⁴`

---

